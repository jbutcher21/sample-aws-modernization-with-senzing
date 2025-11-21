+++
title = "Stage 2: INVENTORY"
weight = 632
+++

## Stage 2: Extract Complete Field Inventory

The AI analyzes the schema file and extracts every single field with data types and sample values. This creates a complete inventory to map in later stages.

::alert[**Critical.*]{type="warning"}

---

## Your Prompt

```bash
Proceed to Stage 2: Extract all fields from the FTM schema
```

Or simply:
```bash
Continue
```

---

## AI Response: Complete Field Inventory

The AI extracts and categorizes all 31 fields from the FTM schema:

### Root Fields (3)
- `id` - string - Unique identifier for each record
- `schema` - string - Record type (Person, Company, Sanction, Ownership, Directorship)
- `properties` - object - Container for all entity attributes

### Person Attributes (15)
- `name` - array of strings - Full name(s)
- `firstName` - array of strings - First name(s)
- `middleName` - array of strings - Middle name(s)
- `lastName` - array of strings - Last name(s)
- `birthDate` - array of strings - Date of birth
- `address` - array of strings - Full address strings
- `email` - array of strings - Email addresses
- `phone` - array of strings - Phone numbers
- `nationality` - array of strings - Nationality/citizenship
- `country` - array of strings - Country association
- `passportNumber` - array of strings - Passport number(s)
- `idNumber` - array of strings - National ID number(s)
- `taxNumber` - array of strings - Tax identification number(s)
- `gender` - array of strings - Gender (Male/Female)
- `alias` - array of strings - Known aliases

### Additional Person Name Fields (2)
- `previousName` - array of strings - Former names
- `weakAlias` - array of strings - Possible aliases (low confidence)

### Company Attributes (4)
- `name` - array of strings - Organization name
- `previousName` - array of strings - Former company names
- `jurisdiction` - array of strings - Country of incorporation
- `incorporationDate` - array of strings - Legal registration date

### Relationship Fields (7)
- `entity` - array of strings - The subject entity in a relationship
- `owner` - array of strings - The owning entity
- `asset` - array of strings - The owned entity
- `director` - array of strings - The person in a directorship
- `organization` - array of strings - The organization in a directorship
- `role` - array of strings - Management role (President, Principal, etc.)
- `percentage` - array of strings - Ownership percentage

### Sanction Metadata (7)
- `program` - array of strings - Sanctions program name
- `authority` - array of strings - Sanctioning authority
- `reason` - array of strings - Reason for sanction
- `listingDate` - array of strings - Date added to sanctions list
- `startDate` - array of strings - Sanction start date
- `endDate` - array of strings - Sanction end date
- `status` - array of strings - Active/Inactive

### Identifier-Specific Fields (Nested in some Person records) (4)
- `holder` - array of strings - Person who holds the identifier
- `type` - array of strings - Identifier type (passport, SSN, driver's license)
- `number` - array of strings - Identifier number
- `country` - array of strings - Issuing country

---

## Integrity Checkpoint

The AI performs a critical validation:

**Extracted Field Count:** 31 unique fields
**Displayed Field Count:** 31 fields shown above

✅ **INTEGRITY CHECK PASSED**: 31 extracted = 31 displayed (no hallucinated fields)

::alert[**Why This Matters**: Without this check, AIs sometimes "invent" fields that seem plausible but don't actually exist in the data. This can cause mapper code to fail or produce incorrect output. Always verify this count matches!]{type="info"}

---

## Key Observations

### 1. Arrays Everywhere
Notice every field is an `array of strings`. FTM format supports multiple values for most attributes:
- Multiple names (legal name, aliases, previous names)
- Multiple addresses (home, business, historical)
- Multiple identifiers (passport from multiple countries)

**Implication for mapping:** Need to iterate through arrays when mapping to Senzing.

### 2. Overloaded Field Names
Some field names appear in multiple schema types with different meanings:
- `name` - Used in Person, Company, Sanction
- `previousName` - Used in Person and Company
- `entity` - References different types depending on schema

**Implication for mapping:** Need schema-aware mapping logic.

### 3. Nested Relationship Pointers
Fields like `entity`, `owner`, `asset`, `director`, `organization` contain **IDs referencing other records**, not actual data.

**Implication for mapping:** Need multi-pass processing to resolve these references.

---

## Validation Checkpoint

Before proceeding, verify:

- ✅ AI extracted exactly 31 fields (not 30, not 32)
- ✅ AI performed integrity check showing counts match
- ✅ All field categories are shown (Root, Person, Company, Relationship, Sanction, Identifier)
- ✅ Data types are noted (mostly arrays of strings)

::alert[**If the count is wrong**: Stop and ask the AI to re-extract fields. Review the schema file manually to identify what was missed or hallucinated.]{type="info"}

---

## Common Issues and Solutions

| Issue | Cause | Solution |
|-------|-------|----------|
| **Wrong field count** | AI hallucinated or skipped fields | Ask AI to re-count and verify against schema |
| **Missing field categories** | Incomplete schema analysis | Request AI list all record types in schema |
| **No integrity check shown** | AI skipped validation step | Explicitly request: "Verify your field count" |
| **Fields from different dataset** | AI using training data | Remind AI: "Extract only from ftm_schema.md" |

---

## Next Stage

With a complete field inventory verified, proceed to **Stage 3: PLANNING** where you'll determine DATA_SOURCE codes and entity type strategy.

**[Continue to Stage 3: PLANNING →](../633_mapplanning/)**
