---
title: "Stage 5: OUTPUTS"
weight: 635
---

## Stage 5: Generate Mapper Code and Documentation

The final stage generates three critical outputs: a mapper Python script, complete mapping documentation, and sample JSON with validation.

---

## Your Prompt

```
Generate the mapper code, documentation, and sample JSON
```

Or:
```
Proceed to Stage 5: Generate outputs
```

---

## AI Response: Three Output Files

The AI generates complete, production-ready files:

### 1. README.md - Usage Instructions

**Purpose:** Quick start guide for using the mapper

**Contents:**
- How to run the mapper
- Expected inputs and outputs
- Validation commands
- Loading instructions

**Example excerpt:**
```markdown
# FTM Watchlist Mapper

## Usage

python3 ftm_mapper.py ftm.jsonl ftm_senzing.jsonl

## Validation

python3 senzing/tools/lint_senzing_json.py ftm_senzing.jsonl
python3 senzing/tools/sz_json_analyzer.py ftm_senzing.jsonl -o analysis.md

## Loading

sz_file_loader -f ftm_senzing.jsonl
```

---

### 2. ftm_mapper.md - Complete Mapping Specification

**Purpose:** Human-readable mapping documentation (source of truth)

**Contents:**
- All field mapping decisions
- Processing logic explanation
- DATA_SOURCE strategy
- Relationship handling approach
- Sample input → output examples

**Why this matters:**
- Documents business logic for auditing
- Helps others understand mapper without reading code
- Serves as test specification
- Can be used to regenerate mapper if needed

---

### 3. ftm_mapper.py - Python Implementation

**Purpose:** Executable mapper that transforms FTM → Senzing JSON

**Key implementation details:**

#### Multi-Pass Processing

```python {copy}
# Pass 1: Process master entities (Person and Company)
for record in ftm_records:
    if record['schema'] == 'Person':
        senzing_entities[record['id']] = map_person(record)
    elif record['schema'] == 'Company':
        senzing_entities[record['id']] = map_company(record)

# Pass 2: Merge Sanction metadata onto Person entities
for record in ftm_records:
    if record['schema'] == 'Sanction':
        entity_id = record['properties']['entity'][0]
        merge_sanction(senzing_entities[entity_id], record)

# Pass 3: Add Ownership relationships
for record in ftm_records:
    if record['schema'] == 'Ownership':
        owner_id = record['properties']['owner'][0]
        asset_id = record['properties']['asset'][0]
        add_rel_pointer(senzing_entities[owner_id], asset_id, 'OWNER_OF')

# Pass 4: Add Directorship relationships
for record in ftm_records:
    if record['schema'] == 'Directorship':
        director_id = record['properties']['director'][0]
        org_id = record['properties']['organization'][0]
        role = map_role(record['properties']['role'][0])  # PRINCIPAL_OF or PRESIDENT_OF
        add_rel_pointer(senzing_entities[director_id], org_id, role)
```

#### Array Handling

FTM properties are arrays, so the mapper iterates through values:

```python {copy}
def map_person(ftm_record):
    features = []

    # Handle multiple names
    for first_name in ftm_record['properties'].get('firstName', []):
        for last_name in ftm_record['properties'].get('lastName', []):
            features.append({
                'NAME_FIRST': first_name,
                'NAME_LAST': last_name
            })

    # Handle multiple phone numbers
    for phone in ftm_record['properties'].get('phone', []):
        features.append({'PHONE_NUMBER': phone})

    return {
        'DATA_SOURCE': 'SANCTIONS',
        'RECORD_ID': f"sanctions-person-{ftm_record['id']}",
        'FEATURES': features
    }
```

#### REL_ANCHOR and REL_POINTER

All master entities get a REL_ANCHOR so they can be referenced:

```python {copy}
features.append({
    'REL_ANCHOR_DOMAIN': 'SANCTIONS',  # or 'CORP_FILINGS'
    'REL_ANCHOR_KEY': record['id']
})
```

Relationships use REL_POINTER to reference other entities:

```python {copy}
features.append({
    'REL_POINTER_DOMAIN': 'CORP_FILINGS',
    'REL_POINTER_KEY': 'company-123',
    'REL_POINTER_ROLE': 'OWNER_OF'
})
```

---

## Sample JSON Output with Validation

The AI generates sample Senzing JSON and validates it with the linter.

### Sample Person Entity (with merged sanction + identifier)

```json {copy}
{
  "DATA_SOURCE": "SANCTIONS",
  "RECORD_ID": "sanctions-person-1006",
  "FEATURES": [
    { "RECORD_TYPE": "PERSON" },
    {
      "NAME_FIRST": "Robert",
      "NAME_LAST": "Smith Sr",
      "NAME_MIDDLE": "E"
    },
    { "DATE_OF_BIRTH": "1954-03-31" },
    { "ADDR_FULL": "123 Main St, Las Vegas" },
    {
      "DRIVERS_LICENSE_NUMBER": "112233",
      "DRIVERS_LICENSE_STATE": "NV"
    },
    {
      "REL_ANCHOR_DOMAIN": "SANCTIONS",
      "REL_ANCHOR_KEY": "sanctions-person-1006"
    }
  ],
  "SANCTION_PROGRAM": "SANCTIONS",
  "SANCTION_AUTHORITY": "Sanctions Authority",
  "SANCTION_REASON": "Category: Fraud",
  "SANCTION_LISTING_DATE": "2017-01-03",
  "SANCTION_STATUS": "Active"
}
```

### Sample Company Entity (with relationships)

```json {copy}
{
  "DATA_SOURCE": "CORP_FILINGS",
  "RECORD_ID": "corp-filings-company-3088",
  "FEATURES": [
    { "RECORD_TYPE": "ORGANIZATION" },
    { "NAME_ORG": "Universal Exports Worldwide" },
    { "NAME_ORG": "Universal Trading Corp", "USAGE_TYPE": "PRIOR" },
    { "ADDR_COUNTRY": "Germany" },
    {
      "REL_ANCHOR_DOMAIN": "CORP_FILINGS",
      "REL_ANCHOR_KEY": "corp-filings-company-3088"
    },
    {
      "REL_POINTER_DOMAIN": "CORP_FILINGS",
      "REL_POINTER_KEY": "corp-filings-company-3089",
      "REL_POINTER_ROLE": "OWNER_OF"
    }
  ],
  "INCORPORATION_DATE": "1998-05-15"
}
```

### Linter Validation

```bash {copy}
python3 senzing/tools/lint_senzing_json.py sample_output.jsonl
```

**Result:** ✅ **PASSED** - No JSON syntax errors

::alert[**Always lint sample output during development!** Finding structural errors early prevents having to fix broken mapper code later.]{type="info"}

---

## Validation Checkpoint

Before running the mapper on actual data, verify:

- ✅ README.md contains usage instructions
- ✅ ftm_mapper.md documents all mapping decisions
- ✅ ftm_mapper.py implements multi-pass processing
- ✅ Sample Person JSON with merged sanction metadata
- ✅ Sample Company JSON with REL_POINTER relationships
- ✅ Sample output passes linter validation

---

## Common Implementation Issues

| Issue | Cause | Solution |
|-------|-------|----------|
| **Missing relationships** | Single-pass processing | Implement multi-pass: masters first, then relationships |
| **Array indexing errors** | Assuming single values | Always iterate: `for value in array:` |
| **KeyError exceptions** | Missing field checks | Use `.get(field, [])` for optional fields |
| **REL_POINTER to non-existent entity** | Pass ordering wrong | Process targets before pointers |
| **NAME_FULL used for companies** | Copy-paste from Person code | Use NAME_ORG for organizations |

---

## Key Learnings from This Stage

### 1. Multi-Pass is Essential
You **cannot** process FTM data in a single pass because:
- Sanction records reference Person IDs
- Ownership records reference Company IDs
- Relationships require both entities to exist first

### 2. Documentation Matters
The `.md` mapping specification is as important as the code:
- Code can have bugs
- Documentation explains **why** decisions were made
- Makes mapper maintainable by others

### 3. Validate Early
Running the linter on sample output catches issues before processing 73 records:
- Missing required fields
- Incorrect JSON structure
- Typos in feature names

### 4. FTM Arrays Require Iteration
Every property is an array, even if most records have single values:
```python {copy}
# WRONG - causes errors when array is empty or has multiple values
name = record['properties']['firstName'][0]

# RIGHT - handles empty, single, or multiple values
for name in record['properties'].get('firstName', []):
    # process each name
```

---

## Next Steps

Now that you have working mapper code and documentation:

1. **Run the mapper** on actual FTM data
2. **Validate output** with linter and analyzer tools
3. **Configure data sources** in Senzing
4. **Load the data** into Senzing
5. **Analyze results** to see entity resolution in action

**[Continue to Step 4: Validate Mapping →](../../64_validatemapping/)**
