---
title: "Stage 1: INIT"
weight: 631
---

## Stage 1: Initialize the Mapping Assistant

The first stage loads all reference materials and tests validation tools. This gives the AI complete knowledge of Senzing's data format, conventions, and validation requirements.

---

## Your Prompt

```
Yes, let's start the AI-assisted mapping workflow for ftm.jsonl
```

Or if starting fresh:
```
Load the Senzing Mapping Assistant and help me map ftm.jsonl to Senzing format
```

---

## AI Response Summary

The AI performs these initialization steps:

### 1. Load Reference Files

The AI loads five critical reference files:

| File | Purpose | Status |
|------|---------|--------|
| **senzing_entity_specification.md** | Complete feature catalog (50+ features) | ✅ Loaded |
| **senzing_mapping_examples.md** | 7 shot examples with patterns | ✅ Loaded |
| **lint_senzing_json.py** | JSON structure validator | ✅ Loaded & Tested |
| **identifier_crosswalk.json** | 12 canonical identifiers + aliases | ✅ Loaded |
| **usage_type_crosswalk.json** | NAME, ADDRESS, PHONE usage types | ✅ Loaded |

### 2. Test Validation Tools

The AI confirms the linter is functional by running a self-test:

```bash
python3 senzing/tools/lint_senzing_json.py --help
```

**Result:** ✅ Tool functional and ready

### 3. Confirm Schema Availability

The AI verifies the schema file exists and is accessible:
```
workspace/watchlist/ftm_schema.md
```

**Result:** ✅ Schema available with 73 records, 5 schema types, 31 fields

---

## What the AI Now Knows

After Stage 1, the AI has complete knowledge of:

**Senzing Features:**
- All 50+ feature attributes (NAME, ADDRESS, identifiers, etc.)
- Proper usage types and formatting conventions
- Special features (REL_ANCHOR, REL_POINTER, RECORD_TYPE)

**Mapping Patterns:**
- 7 complete worked examples showing common patterns
- How to handle names, addresses, identifiers, dates
- When to use features vs payload attributes

**Identifier Standards:**
- Canonical identifier names (SSN_NUMBER, PASSPORT_NUMBER, etc.)
- Common aliases (SSN = social_security_number = taxpayer_id)
- International identifier types

**Validation Requirements:**
- Required fields (DATA_SOURCE, RECORD_ID)
- JSON structure rules
- Feature attribute naming conventions

---

## Validation Checkpoint

::alert[**Verify**: The AI should explicitly list all 5 files it loaded. If it skips any or says a file is unavailable, stop and troubleshoot before proceeding.]{type="info"}

The AI should confirm:
- ✅ All 5 reference files loaded successfully
- ✅ Linter tool is functional
- ✅ Schema file is accessible
- ✅ Ready to proceed to Stage 2

---

## Key Learning Point

**Why separate initialization from mapping?**

This staged approach prevents common AI mapping errors:
1. **Hallucination prevention**: AI uses actual documentation instead of outdated training data
2. **Convention adherence**: AI follows current Senzing standards, not assumptions
3. **Tool readiness**: Validation tools are tested before generating output
4. **Explicit knowledge**: You see exactly what the AI knows before it starts making decisions

::alert[**Compare to Exercise 1**: In the customer mapping exercise, this stage was shown with detailed screenshots of each file being loaded. Here, we summarize the result. The underlying process is identical.]{type="info"}

---

## Common Issues and Solutions

| Issue | Cause | Solution |
|-------|-------|----------|
| **File not found error** | Wrong working directory | Verify you're in the workshop root directory |
| **Linter test fails** | Python environment issue | Check Python 3 is available: `python3 --version` |
| **AI skips files** | Prompt not clear | Explicitly request: "Load all 5 reference files" |
| **AI uses old knowledge** | Not following prompt | Restart and emphasize: "Use ONLY the loaded reference files" |

---

## Next Stage

Once initialization is complete, proceed to **Stage 2: INVENTORY** where the AI extracts all fields from the FTM schema.

**[Continue to Stage 2: INVENTORY →](../632_mapinventory/)**
