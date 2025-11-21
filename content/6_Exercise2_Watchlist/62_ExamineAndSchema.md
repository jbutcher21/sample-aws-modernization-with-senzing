+++
title = "Step 2: Examine Source Data and Generate Schema"
weight = 62
+++

## Understanding the FTM Watchlist Data

Before mapping any data to Senzing format, you need to understand its structure. Unlike the customer CSV file in Exercise 1, this watchlist data is in **FollowTheMoney (FTM) JSON format** - a more complex format with nested structures and relationships.

::alert[**FTM Format.*]{type="info"}

---

## Examine the Source File

The watchlist data is located at:
```
workspace/watchlist/ftm.jsonl
```

**Format Characteristics:**
- **JSONL** (JSON Lines) - One JSON object per line
- **Nested structures** - Complex objects with properties arrays
- **Multiple schema types** - Person, Company, Sanction, Ownership, Directorship
- **International data** - Arabic and Cyrillic character sets
- **Relationship pointers** - Entities reference other entities by ID

**Sample FTM Record:**
```json
{
  "id": "sanctions-person-1006",
  "schema": "Person",
  "properties": {
    "name": ["Robert Smith Sr"],
    "firstName": ["Robert"],
    "middleName": ["E"],
    "lastName": ["Smith Sr"],
    "birthDate": ["1954-03-31"],
    "address": ["123 Main St, Las Vegas"],
    "phone": ["702-555-0123"],
    "email": ["rsmith@example.com"]
  }
}
```

---

## Generate the Schema

**Your Prompt:**
```bash
Generate a schema for the ftm.jsonl file I have open
```

**AI Response:**

The AI will run the schema generator tool:

```bash
python3 senzing/tools/sz_schema_generator.py workspace/watchlist/ftm.jsonl -o workspace/watchlist/ftm_schema.md
```

::alert[**Why Generate.*]{type="info"}

---

## Schema Analysis Results

### Overview Statistics

| Metric | Value |
|--------|-------|
| **Total Records** | 73 |
| **Schema Types** | 5 (Person, Sanction, Company, Ownership, Directorship) |
| **Unique Fields** | 31 |
| **Character Sets** | Latin, Cyrillic, Arabic |

### Record Type Breakdown

| Schema Type | Count | Purpose |
|-------------|-------|---------|
| **Person** | 33 | Individual entities (people) |
| **Sanction** | 17 | Sanctions metadata for persons |
| **Company** | 6 | Organization entities |
| **Ownership** | 8 | Company ownership relationships |
| **Directorship** | 6 | Company management relationships |

### Complete Field Inventory

**Root Fields:**
- `id` - Unique identifier for each record
- `schema` - Record type (Person, Company, Sanction, etc.)
- `properties` - Container for all attributes

**Person Attributes:**
- `name`, `firstName`, `middleName`, `lastName` - Name fields
- `birthDate` - Date of birth
- `address` - Full address strings
- `email`, `phone` - Contact information
- `nationality`, `country` - Geographic data
- `passportNumber`, `idNumber`, `taxNumber` - Identifiers
- `gender` - Male/Female
- `alias`, `previousName`, `weakAlias` - Name variations

**Company Attributes:**
- `name` - Organization name
- `jurisdiction` - Country of incorporation
- `incorporationDate` - Legal registration date
- `address` - Business address
- `previousName` - Former names

**Relationship Fields:**
- `entity` - The subject of a sanction or relationship
- `owner` - The owning entity in an ownership relationship
- `asset` - The owned entity in an ownership relationship
- `director` - The person in a directorship
- `organization` - The organization in a directorship
- `role` - Management role (e.g., "President", "Principal")
- `percentage` - Ownership percentage

**Sanction Metadata:**
- `program` - Sanctions program name
- `authority` - Sanctioning authority
- `reason` - Reason for sanction
- `listingDate` - Date added to sanctions list
- `startDate`, `endDate` - Sanction period
- `status` - Active/Inactive

**Identifier Fields (nested in Person records):**
- `holder` - Person who holds the identifier
- `type` - Identifier type (passport, SSN, driver's license)
- `number` - Identifier number
- `country` - Issuing country

---

## Key Differences from Customer CSV

| Aspect | Customer CSV (Exercise 1) | FTM Watchlist (Exercise 2) |
|--------|---------------------------|---------------------------|
| **Format** | Flat CSV (one row = one record) | Nested JSON (arrays, objects) |
| **Complexity** | Simple - 19 fields per record | Complex - 31 fields across 5 schemas |
| **Entity Types** | All in one file | Separated by schema type |
| **Relationships** | None | Explicit (Ownership, Directorship) |
| **Character Sets** | English only | Multilingual (Cyrillic, Arabic) |
| **Processing** | Single-pass | Multi-pass (merge relationships) |

---

## What This Means for Mapping

The schema analysis reveals several mapping challenges:

1. **Multiple Schema Types**: Need to decide which are "master entities" vs "metadata" vs "relationships"
2. **Nested Structures**: Properties are arrays, not simple strings
3. **Relationship Pointers**: Some records reference other records by ID
4. **Mixed Entity Types**: Both Person and Organization entities in same dataset
5. **International Data**: Name transliteration and format variations

::alert[**Important**: This is significantly more complex than the customer CSV! The FTM format requires a **multi-pass processing strategy** where you:
1. Process master entities (Person, Company)
2. Merge metadata records (Sanction) onto masters
3. Convert relationship records (Ownership, Directorship) to REL_POINTER format]{type="warning"}

---

## Next Steps

Now that you understand the data structure, you're ready to map it to Senzing format using the AI-assisted mapping workflow. The next section walks through the 5-stage Senzing Mapping Assistant process.

::alert[**Pro Tip**.*]{type="info"}
