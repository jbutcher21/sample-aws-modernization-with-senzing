+++
title = "Step 4: Validate Mapping"
weight = 64
+++

## Run the Mapper and Validate Output

Now it's time to run the mapper on the actual FTM data and validate the results using Senzing's validation tools.

---

## Step 1: Run the Mapper

Execute the mapper script on the actual FTM watchlist data:

```bash
python3 ftm_mapper.py ftm.jsonl ftm_senzing.jsonl
```

**Expected Output:**
```
Processing 73 FTM records...
Pass 1: Processing master entities (Person, Company)...
  Created 33 Person entities
  Created 6 Company entities
Pass 2: Merging Sanction metadata...
  Merged 17 sanctions onto Person entities
Pass 3: Adding Ownership relationships...
  Added 8 ownership relationships
Pass 4: Adding Directorship relationships...
  Added 6 directorship relationships

✅ Generated 39 Senzing entities from 73 FTM records
✅ Output written to: ftm_senzing.jsonl
```

{{% notice warning %}}**39 entities from 73 records:** This is expected! Sanction, Ownership, and Directorship records aren't separate entities - they're metadata and relationships merged onto the 39 master entities (33 Person + 6 Company).]{type="info"}

---

## Step 2: Validate JSON Structure (Linter)

First validation: Check that the JSON is structurally correct:

```bash
python3 senzing/tools/lint_senzing_json.py ftm_senzing.jsonl
```

**Expected Result:**
```
✅ PASSED - No JSON syntax errors
All records have required fields (DATA_SOURCE, RECORD_ID)
```

{{% notice info %}}**What the linter checks:**
- Valid JSON syntax (no missing commas, brackets, etc.)
- Required fields present (DATA_SOURCE, RECORD_ID)
- FEATURES array structure correct
- No obvious structural issues{{% /notice %}}

---

## Step 3: Analyze Data Quality

Second validation: Check that Senzing will recognize and use the mapped data:

```bash
python3 senzing/tools/sz_json_analyzer.py ftm_senzing.jsonl -o analysis.md
```

{{% notice info %}}**Important:** According to the tools reference documentation, the analyzer outputs to a `.md` file. You must then **read the markdown file** to see the results, not just look at console output!{{% /notice %}}

Read the analysis results:

```bash
cat analysis.md
```

**Initial Result:**
```
❌ Critical Errors: 2

ERROR: DATA_SOURCE not found: CORP_FILINGS
ERROR: DATA_SOURCE not found: SANCTIONS

✅ Feature Attributes: 13 Senzing features recognized
  - NAME_FIRST (25 records)
  - NAME_LAST (25 records)
  - NAME_ORG (6 records)
  - DATE_OF_BIRTH (18 records)
  - ADDR_FULL (22 records)
  - PHONE_NUMBER (31 records)
  - EMAIL_ADDRESS (15 records)
  ...

⚠️ Warnings: 3
  - Some optional features have low population (expected)
```

---

## Step 4: Fix Critical Errors

The analyzer found **critical errors**: DATA_SOURCE codes not registered in Senzing.

{{% notice warning %}}**Critical vs Non-Critical:**
- **Critical errors** (red) - Must fix before loading. Senzing will reject the data.
- **Warnings** (orange) - Should review but don't block loading.
- **Info** (yellow) - Payload attributes, expected and fine.{{% /notice %}}

### Configure Data Sources

Create a configuration file to register both DATA_SOURCE codes:

```bash
cat > ftm_config.g2c << 'EOF'
addDataSource CORP_FILINGS
addDataSource SANCTIONS
save
EOF
```

Run the configuration tool:

```bash
source ~/.bashrc && sz_configtool -f ftm_config.g2c
```

**Expected Output:**
```
Loading configuration commands from ftm_config.g2c...
Adding data source: CORP_FILINGS
  ✅ Data source CORP_FILINGS added (DSRC_ID: 1001)
Adding data source: SANCTIONS
  ✅ Data source SANCTIONS added (DSRC_ID: 1002)
Saving configuration...
  ✅ Configuration saved successfully
```

---

## Step 5: Re-analyze After Fix

Run the analyzer again to confirm errors are resolved:

```bash
python3 senzing/tools/sz_json_analyzer.py ftm_senzing.jsonl -o analysis.md
cat analysis.md
```

**Final Result:**
```
✅ Critical Errors: 0 (resolved!)

✅ Feature Attributes: 13 Senzing features with good coverage
  GREEN - Recognized and will be used for matching:
    - NAME_FIRST (25 records, 64%)
    - NAME_LAST (25 records, 64%)
    - NAME_ORG (6 records, 100%)
    - DATE_OF_BIRTH (18 records, 46%)
    - ADDR_FULL (22 records, 56%)
    - PHONE_NUMBER (31 records, 79%)
    - EMAIL_ADDRESS (15 records, 38%)
    - SSN_NUMBER (2 records, 5%)
    - DRIVERS_LICENSE_NUMBER (1 record, 3%)
    - PASSPORT_NUMBER (8 records, 21%)
    - NATIONAL_ID_NUMBER (3 records, 8%)
    - REL_ANCHOR_DOMAIN (39 records, 100%)
    - REL_POINTER_DOMAIN (12 records, 31%)

✅ Payload Attributes: 6 custom attributes
  YELLOW - Will be stored but not used for matching:
    - SANCTION_PROGRAM (17 records)
    - SANCTION_AUTHORITY (17 records)
    - SANCTION_REASON (17 records)
    - SANCTION_LISTING_DATE (17 records)
    - SANCTION_STATUS (17 records)
    - INCORPORATION_DATE (4 records)

⚠️ Warnings: Expected low population on optional features
  ORANGE - Not a problem, just informational:
    - SSN_NUMBER only in 5% of records (expected - international data)
    - PASSPORT_NUMBER only in 21% of records (expected - incomplete data)

Ready to load into Senzing!
```

::alert[**Understanding the Color Codes:**
- **GREEN** - Feature attributes recognized by Senzing, will be used for matching
- **YELLOW** - Payload attributes, stored with entity but don't affect matching
- **ORANGE** - Warnings about data coverage (usually expected)
- **RED** - Critical errors that must be fixed{{% /notice %}}

---

## Validation Summary

After completing all validation steps, you should have:

| Validation | Tool | Result |
|------------|------|--------|
| ✅ **JSON Structure** | lint_senzing_json.py | PASSED |
| ✅ **Data Sources** | sz_json_analyzer.py | 0 critical errors |
| ✅ **Feature Coverage** | sz_json_analyzer.py | 13 features recognized |
| ✅ **Payload Attributes** | sz_json_analyzer.py | 6 attributes will be stored |
| ✅ **Relationships** | sz_json_analyzer.py | REL_ANCHOR (39), REL_POINTER (12) |

**Status:** ✅ **Ready to load into Senzing**

---

## Common Validation Issues

| Issue | Cause | Solution |
|-------|-------|----------|
| **DATA_SOURCE not found** | Not registered in Senzing config | Use sz_configtool to add data sources |
| **Unrecognized features** | Typo in feature name | Check spelling against entity spec |
| **All attributes showing as yellow** | Forgot FEATURES array | Wrap features in FEATURES array |
| **No REL_ANCHOR found** | Missing relationship setup | Add REL_ANCHOR to master entities |
| **REL_POINTER pointing to nothing** | Target entity doesn't exist | Check multi-pass processing order |

---

## Key Learnings

### Two-Layer Validation
Senzing provides two distinct validation tools for different purposes:
1. **Linter** - Checks JSON structure and required fields
2. **Analyzer** - Checks Senzing-specific quality (data sources, features, coverage)

Both are necessary! Linter catches syntax errors, analyzer catches semantic issues.

### Critical vs Warning
Not all analyzer output is equally important:
- **Critical errors (red)** - Must fix, data will be rejected
- **Warnings (orange)** - Review but often expected (e.g., sparse optional fields)
- **Info (yellow)** - Payload attributes, completely fine

Don't panic at yellow/orange output - read what it says!

### Configuration is Part of Validation
Data sources must be registered before loading. This is a configuration step, not a data issue. The analyzer catches this before you try to load data and get cryptic errors.

---

## Next Step

With validation complete and all critical errors resolved, you're ready to load the data into Senzing and see entity resolution in action!

**[Continue to Step 5: Load Data →](../65_loaddata/)**
