+++
title = "Step 5: Load Data into Senzing"
weight = 65
+++

## Load Mapped Data and Take Snapshot

With validation complete and all critical errors resolved, load the watchlist data into Senzing to perform entity resolution.

---

## Step 1: Load the Data

Use the Senzing file loader to import the mapped JSONL:

```bash
source ~/.bashrc && sz_file_loader -f ftm_senzing.jsonl
```

**Expected Output:**
```
Loading records from ftm_senzing.jsonl...

Processing: |████████████████████████████████████████| 100%

Load Summary:
  Records loaded:        39
  Records failed:         0
  Processing time:        0.0 minutes

Entity Resolution Statistics:
  Candidate matches evaluated:  259
  Ambiguous matches detected:     5

✅ Load completed successfully
```

{{% notice info %}}**What Just Happened:**
- All 39 records loaded successfully (no data errors)
- Senzing evaluated 259 potential matches across all data sources
- 5 matches were "ambiguous" (could match multiple ways - Senzing will flag these)
- Processing took under 1 minute (this is a small dataset){{% /notice %}}

---

## Understanding the Load Statistics

### Records Loaded: 39
This is the watchlist data (33 Person + 6 Company), but remember:
- You already had 120 customer records loaded (from Exercise 1)
- Total records now in Senzing: **159** (120 + 39)
- This enables **cross-source matching** between customers and watchlist!

### Candidate Matches: 259
Senzing compared these new 39 records against:
- Each other (watchlist-to-watchlist matches)
- The existing 120 customer records (watchlist-to-customer matches)
- Generated 259 pairwise comparisons that met matching thresholds

### Ambiguous Matches: 5
Some records could match in multiple ways. Senzing flags these for human review:
- Same person with slightly different data in multiple sources?
- Actually different people who happen to have similar attributes?
- Legitimate uncertainty that requires business judgment

---

## Step 2: Take a Snapshot

Capture the current entity resolution state for analysis:

```bash
source ~/.bashrc && sz_snapshot -o ftm-watchlist-snapshot-$(date +%Y-%m-%d) -Q
```

**Expected Output:**
```
Generating snapshot: ftm-watchlist-snapshot-2025-11-16.json
Analyzing entity resolution statistics...

Snapshot complete:
  Total data sources:    3 (CUSTOMERS, SANCTIONS, CORP_FILINGS)
  Total records:       159
  Total entities:       92
  Overall compression:  42.1%
  Cross-source matches: 17

✅ Snapshot written to: ftm-watchlist-snapshot-2025-11-16.json
```

{{% notice info %}}**What is a Snapshot?**
A snapshot is a JSON file containing comprehensive entity resolution statistics:
- Record and entity counts by data source
- Compression rates (how many duplicates were found)
- Cross-source matches (same entity in multiple systems)
- Relationship counts
- Match quality breakdown (definitive, possible, ambiguous){{% /notice %}}

---

## Interpreting the Snapshot Statistics

### 159 Records → 92 Entities (42.1% Compression)

**What this means:**
- 159 total source records were loaded
- Senzing determined they represent only 92 unique real-world entities
- **42.1% of records were duplicates** of entities already known
- 67 records merged into existing entities

**This is significant compression!** Almost half the records were recognized as duplicates.

### Cross-Source Matches: 17

**What this means:**
- 17 entities have records from **multiple data sources**
- Examples:
  - A person appears in both CUSTOMERS and SANCTIONS (watchlist hit!)
  - A person appears in both CUSTOMERS and CORP_FILINGS (customer is a company officer)
  - A person appears in SANCTIONS and CORP_FILINGS (sanctioned individual owns a company)

These cross-source matches are the **most interesting findings** from entity resolution!

---

## Step 3: Quick Verification

Verify the data loaded correctly by checking record counts:

```bash
source ~/.bashrc && sz_explorer -query 'DATA_SOURCE=SANCTIONS'
```

**Expected:**
- Should return entities that have SANCTIONS records
- Verify some have merged sanction payload attributes
- Check that relationships are present

```bash
source ~/.bashrc && sz_explorer -query 'DATA_SOURCE=CORP_FILINGS'
```

**Expected:**
- Should return company entities
- Verify organization names appear correctly
- Check for ownership relationships

---

## Common Loading Issues

| Issue | Cause | Solution |
|-------|-------|----------|
| **DATA_SOURCE not found errors** | Data sources not configured | Re-run sz_configtool with data source commands |
| **All records fail to load** | JSON structure errors | Re-run linter to find syntax problems |
| **Some records fail** | Invalid data in specific records | Check error log for record IDs and field issues |
| **Load seems stuck** | Large dataset processing | Be patient, or check with `top` command |
| **Duplicate record errors** | RECORD_ID collision | Ensure RECORD_IDs are unique within DATA_SOURCE |

---

## Success Indicators

You know the load was successful if:

- ✅ **Records loaded = 39, Records failed = 0**
- ✅ **Snapshot generates without errors**
- ✅ **Total entities < Total records** (compression detected)
- ✅ **Cross-source matches > 0** (found connections between data sources)
- ✅ **Explorer queries return results** for both SANCTIONS and CORP_FILINGS

---

## What Happens During Loading?

### 1. Record Ingestion
Senzing reads each JSON record and extracts features and payload attributes.

### 2. Entity Resolution
For each record, Senzing:
- Generates match candidates based on features (name, address, phone, identifiers, etc.)
- Scores each candidate match using ML algorithms
- Determines if record matches existing entity or creates new one
- Updates entity with new information from record

### 3. Relationship Processing
For records with REL_POINTER:
- Links entities together with typed relationships
- Builds network graph of connections
- Enables relationship path finding and network expansion

### 4. Indexing
All features, payload attributes, and relationships are indexed for fast querying.

---

## Key Learnings

### Load Time Scales
39 records loaded in < 1 minute. Performance varies by:
- **Record complexity** (features, relationships, payload)
- **Dataset size** (existing entities to compare against)
- **Hardware** (CPU, memory, disk)

For reference:
- Thousands of records: minutes
- Millions of records: hours (but can parallelize)

### Cross-Source Matching is Automatic
You didn't do anything special to enable watchlist-to-customer matching. Senzing automatically:
- Compared new SANCTIONS records against existing CUSTOMERS
- Compared new CORP_FILINGS against both CUSTOMERS and SANCTIONS
- Found matches based on feature similarity (names, phones, addresses, etc.)

### Compression Indicates Quality
42% compression suggests:
- Good data quality (clean enough to match)
- Realistic duplicates (not over-matching)
- Effective feature mapping (right attributes used for matching)

Low compression (<10%) might indicate:
- Very clean, de-duplicated source data
- Under-matching (not enough features, or thresholds too strict)

Very high compression (>80%) might indicate:
- Very dirty data with many duplicates
- Over-matching (false positives, thresholds too loose)

---

## Next Steps

With data loaded and snapshot captured, you're ready to analyze the entity resolution results in detail!

**The next section demonstrates an important lesson about working with AI across sessions...**

**[Continue to Step 6: Analyze Snapshot →](../66_analyzesnapshot/)**
