---
title: "Validation Tools"
chapter: false
weight: 34
---

## Verify Your Mappings Are Correct

Data mapping isn't complete until it's validated. This workshop includes three essential tools that verify your mappings at different stages of the process.

## The Three Validation Tools

### 1. Schema Generator - `sz_schema_generator.py`

**Purpose**: Analyze source data structure before mapping

**What it does:**
- Scans your source data file (CSV or JSON)
- Generates field-by-field analysis showing:
  - Field names and data types
  - Population percentage (% of records with values)
  - Uniqueness (% of distinct values)
  - Sample values
  - Min/max lengths

**When to use:** Before mapping (Stage 2 - INVENTORY) to understand your source data

**Example:**
```bash
cd workshop/senzing/tools
python3 sz_schema_generator.py ../../workspace/customers/customers.csv
```

**Output:** Markdown file with complete schema documentation

---

### 2. JSON Linter - `lint_senzing_json.py`

**Purpose**: Validate Senzing JSON structure and syntax

**What it does:**
- Verifies JSON is well-formed
- Checks required fields exist (DATA_SOURCE, RECORD_ID)
- Validates feature structure
- Catches common formatting errors
- Reports warnings and errors

**When to use:** After mapping (Stage 5) to verify output format is correct

**Example:**
```bash
cd workshop/senzing/reference
python3 lint_senzing_json.py ../../solutions/customers/customers_senzing.jsonl
```

**Output:** Either "OK: All files passed" or detailed error messages

---

### 3. JSON Analyzer - `sz_json_analyzer.py`

**Purpose**: Show what Senzing will actually recognize in your data

**What it does:**
- Uses cached Senzing configuration to analyze mapped data
- Shows which attributes Senzing recognizes (GREEN)
- Shows which attributes are payload/unmapped (YELLOW)
- Flags errors like unregistered DATA_SOURCE (RED)
- Warns about sparse optional fields (ORANGE)
- Provides statistics on record counts and coverage

**When to use:** After linting passes, to see what Senzing sees

**Example:**
```bash
cd workshop/senzing/tools
python3 sz_json_analyzer.py ../../solutions/customers/customers_senzing.jsonl
```

**Output:** Color-coded report showing:
- **GREEN**: Mapped Senzing features (will be used for entity resolution)
- **YELLOW**: Unmapped attributes (payload data, stored but not matched)
- **RED**: Errors (missing DATA_SOURCE registration, invalid values)
- **ORANGE**: Warnings (sparse data, unusual patterns)

---

## Validation Workflow

The typical validation sequence:

```
1. Generate schema → Understand source data
2. Map with AI assistance → Create mapper
3. Run mapper → Generate Senzing JSON
4. Run linter → Verify JSON structure
5. Run analyzer → Verify Senzing will recognize everything
6. Fix any issues → Re-run steps 3-5
7. Load into Senzing → See entity resolution results
```

{{% notice tip %}}
**Always validate in this order**: Linter first (structure), then analyzer (semantics). If the linter fails, the analyzer results won't be meaningful.
{{% /notice %}}

## Tool Locations

All three tools are in the `workshop/senzing/` directory:

```
workshop/senzing/
├── tools/
│   ├── sz_schema_generator.py    # Analyze source data
│   ├── sz_json_analyzer.py        # Analyze mapped data
│   └── g2config.json              # Cached Senzing config
└── reference/
    └── lint_senzing_json.py       # Validate JSON structure
```

## Example Validation Output

**Linter Success:**
```
Linting file: customers_senzing.jsonl

OK: All files passed
```

**Analyzer Success Indicators:**
- All expected features shown in GREEN
- Payload attributes in YELLOW (expected)
- No RED errors (or only DATA_SOURCE not registered, which is normal before loading)
- Statistics match your record count

**What "Good" Looks Like:**
- ✅ Linter passes with no errors
- ✅ All features recognized (GREEN)
- ✅ Payload correctly identified (YELLOW)
- ✅ No missing required fields
- ✅ Record count matches source data

---

## Hands-On Practice Coming Next

In Module 4, you'll use all three tools as you map the customer dataset:
1. Review the pre-generated schema
2. Map fields with AI assistance
3. Validate with linter and analyzer
4. Iterate until everything passes

**Important**: Don't skip validation! It's the only way to know your mapping is correct before loading thousands of records into Senzing.

Ready to start mapping? Let's move to Module 4!
