+++
title = "Stage 3: PLANNING"
weight = 633
+++

## Stage 3: Determine DATA_SOURCE and Processing Strategy

Before mapping individual fields, you need to make high-level decisions about how to structure the data in Senzing. This stage determines DATA_SOURCE codes, entity types, and the overall processing strategy.

---

## Your Prompt

```
Proceed to Stage 3: Determine DATA_SOURCE codes and entity types
```

---

## AI Initial Response

The AI analyzes the five FTM schema types and proposes a strategy:

### Master Entity Types

**Master entities** are the primary records that will become Senzing entities:

| Schema Type | Count | Maps To | DATA_SOURCE |
|-------------|-------|---------|-------------|
| **Person** | 33 | Person entities | SANCTIONS |
| **Company** | 6 | Organization entities | CORP_FILINGS |

### Relationship Types

**Relationship records** reference master entities and will be processed differently:

| Schema Type | Count | Processing Strategy |
|-------------|-------|---------------------|
| **Sanction** | 17 | Merge as payload attributes onto Person entities |
| **Ownership** | 8 | Convert to REL_POINTER relationships |
| **Directorship** | 6 | Convert to REL_POINTER relationships |

---

## Your Correction

{{% notice warning %}}**Teaching Moment**: The AI initially said "3 master entity types" but only listed 2 (Person and Company). This is exactly the kind of error you should catch and correct!{{% /notice %}}

**Your prompt:**
```
You say 3 master entity types but list 2: person and company. What is the third?
```

**AI Response:**
```
You're absolutely correct - that was an error on my part. Let me correct the Stage 2 summary:

CORRECTED: 2 master entity types (Person, Company)
          3 relationship types (Sanction, Ownership, Directorship)

I conflated "master entities" with "relationship types". Thank you for catching that!
```

{{% notice info %}}**Key Learning**: Always verify AI counts and categorizations. Simple arithmetic errors can indicate deeper misunderstandings that will cause problems later.{{% /notice %}}

---

## Final Strategy

### DATA_SOURCE Codes

Two separate DATA_SOURCE codes reflect the different domains:

**SANCTIONS**
- All Person entities (33 records)
- Represents watchlist/sanctions domain
- RECORD_ID format: `sanctions-person-{id}`

**CORP_FILINGS**
- All Company entities (6 records)
- Represents corporate registry domain
- RECORD_ID format: `corp-filings-company-{id}`

{{% notice info %}}**Why separate DATA_SOURCE codes?** This allows Senzing to track which system contributed which information. When a Person from SANCTIONS matches a director in CORP_FILINGS, you can see both sources in the resolved entity.{{% /notice %}}

### Processing Strategy: Multi-Pass

The FTM data requires **three-pass processing** because some records are metadata or relationships:

**Pass 1: Master Entities**
- Process all Person and Company records
- Create Senzing records with REL_ANCHOR

**Pass 2: Sanction Metadata**
- Match Sanction records to their Person entities (via `entity` field)
- Merge sanction attributes as payload onto existing Person records

**Pass 3: Relationships**
- Process Ownership and Directorship records
- Add REL_POINTER relationships to existing entities

**Pass 4: Identifier Records** *(if present in data)*
- Merge identifier details onto Person entities

### Entity Type Determination

**PERSON entities:**
- All records from Person schema type
- `RECORD_TYPE: "PERSON"` in Senzing output

**ORGANIZATION entities:**
- All records from Company schema type
- `RECORD_TYPE: "ORGANIZATION"` in Senzing output

---

## Validation Checkpoint

Before proceeding to field mapping, confirm:

- ✅ Two DATA_SOURCE codes identified: SANCTIONS, CORP_FILINGS
- ✅ Two master entity types: Person (PERSON), Company (ORGANIZATION)
- ✅ Three relationship/metadata types: Sanction, Ownership, Directorship
- ✅ Multi-pass processing strategy understood
- ✅ Arithmetic errors corrected (2 master types, not 3)

---

## Key Planning Decisions Explained

### Why SANCTIONS and CORP_FILINGS?

**SANCTIONS:**
- Primary source is watchlist/sanctions data
- Even persons not directly sanctioned are in a sanctions-related dataset
- Makes it clear this data comes from compliance/risk domain

**CORP_FILINGS:**
- Companies come from corporate registry information
- Separates legal entity data from person data
- Allows tracking which company information came from which filing

### Why Not All One DATA_SOURCE?

You *could* use a single DATA_SOURCE like "FTM_WATCHLIST", but separating by domain provides benefits:
- Clearer data provenance (which system contributed what)
- Better cross-source matching visibility
- Easier debugging when issues arise
- More accurate record counts by source system

### Why Multi-Pass Processing?

**Single-pass processing won't work** because:
- Sanction records reference Person IDs that must exist first
- Ownership records reference Company IDs
- Directorship records reference both Person and Company IDs

Processing in passes ensures all referenced entities exist before relationships are added.

---

## Common Issues and Solutions

| Issue | Cause | Solution |
|-------|-------|----------|
| **Too many DATA_SOURCE codes** | Over-segmentation | Group by logical source system, not record type |
| **Unclear entity vs metadata** | Confused relationship types | Ask: "Does this become its own Senzing entity?" |
| **Single-pass assumption** | Missed relationship pointers | Check for fields that reference other record IDs |
| **Arithmetic doesn't match** | AI counting error | Verify counts against schema file |

---

## Next Stage

With the high-level strategy confirmed, proceed to **Stage 4: MAPPING** where you'll make field-by-field disposition decisions.

**[Continue to Stage 4: MAPPING →](../634_mapmapping/)**
