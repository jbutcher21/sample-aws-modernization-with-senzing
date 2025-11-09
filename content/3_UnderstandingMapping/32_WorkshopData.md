---
title: "Your Workshop Datasets"
chapter: false
weight: 32
---

## Two Datasets for Learning

This workshop includes two datasets that you'll map to Senzing format:

### 1. Customer Data (Core Exercise - Module 4)

**File**: `workshop/workspace/customers/customers.csv`

This is a realistic customer database export with **120 records** containing a mix of individual persons (114) and organizations (6). The data includes:

**Core Fields:**
- Customer ID and name
- Customer type indicator (Individual or Company)

**Demographics** (for persons):
- Gender and date of birth

**Contact Information:**
- Address (street, city, state, zip, country)
- Phone numbers
- Email addresses

**Identifiers:**
- Dynamic identifier fields (SSN, Driver's License, Passport, National ID)
- Stored as: `id_type`, `id_number`, `id_country`

**Payload Attributes** (not used for matching):
- Customer registration date
- Account status
- Account balance
- Customer tier

**Data Quality**: Like real-world data, this dataset has varying completeness - not every field is populated for every record.

### 2. Watchlist Data (Bonus Exercise - Module 6)

**File**: `workshop/workspace/watchlist/ftm.jsonl`

This is **70 entities** in FollowTheMoney (FTM) format representing international watchlist records. This dataset is more complex:

**Entity Types:**
- 33 Person entities
- 6 Company entities
- 17 Sanction relationships
- 8 Ownership relationships
- 6 Directorship relationships

**Challenges:**
- Nested JSON structure (properties as arrays)
- Multiple entity types in one file
- Relationships between entities
- International names (various scripts and languages)

This advanced dataset teaches you to map complex formats and handle entity relationships.

## Pre-Generated Schema Analysis

To help you understand the data structure, pre-generated schema files are available:

- **Customer Schema**: `workshop/solutions/customers/customers_schema.md`
  - Field-by-field analysis
  - Population percentages
  - Sample values
  - Data type detection

- **Watchlist Schema**: `workshop/solutions/watchlist/ftm_schema.md`
  - FTM structure breakdown
  - Entity type distribution
  - Property analysis

{{% notice info %}}
These schema files were generated using `workshop/senzing/tools/sz_schema_generator.py` - a tool you'll use when mapping your own data.
{{% /notice %}}

## Viewing the Data

You can explore the datasets directly in your Cloud9 environment:

**View customer data:**
```bash
cd workshop/workspace/customers
head -20 customers.csv
```

**View watchlist data:**
```bash
cd workshop/workspace/watchlist
head -5 ftm.jsonl | python3 -m json.tool
```

**Review schemas:**
```bash
cat workshop/solutions/customers/customers_schema.md | head -50
```

Take a few minutes to familiarize yourself with the data structure before proceeding to learn the mapping workflow.

Ready to learn how the AI-assisted mapping process works?
