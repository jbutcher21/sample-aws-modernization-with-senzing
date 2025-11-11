---
title: "Bonus: Map Watchlist Data"
chapter: true
weight: 6
---

# Bonus: Map Watchlist Data

## Overview

Ready for a challenge? In this optional bonus module, you'll map watchlist data in FollowTheMoney (FTM) format to Senzing. This is more complex than the customer mapping because it includes:

- **Nested structures** - Properties stored as arrays
- **Multiple entity types** - Person, Company, Sanction, Ownership, Directorship
- **Relationships** - How entities connect to each other
- **International names** - Names in various scripts (Arabic, Cyrillic, Chinese)

## Why This Matters

Real-world entity resolution often involves:
- Watchlist screening (sanctions, PEPs, adverse media)
- Corporate structures (ownership, directorships)
- Cross-border entities (multiple languages, naming conventions)

Learning to map FTM format prepares you for these scenarios.

## The Challenge

**Source Data:**
- `workspace/watchlist/ftm.jsonl` - 70 entities in FollowTheMoney format
- Pre-analyzed schema: `solutions/watchlist/ftm_schema.md`

**Entity Breakdown:**
- 33 Person entities
- 6 Company entities
- 17 Sanction relationships
- 8 Ownership relationships
- 6 Directorship relationships

**Complexity:**
- Properties are nested arrays: `{"properties": {"name": ["John Smith"]}}`
- Multiple record types in one file
- Relationships reference other entity IDs
- International character encoding

## What You'll Do

1. **Analyze FTM Structure** - Understand the nested format
2. **Map Entities** - Person and Company entities first
3. **Map Relationships** - Sanction, Ownership, Directorship
4. **Flatten Arrays** - Extract values from FTM property arrays
5. **Handle References** - Deal with entity relationships
6. **Validate** - Ensure all 70 entities mapped correctly

## Using the Mapping Assistant

The same Senzing Mapping Assistant workflow applies:

1. **STAGE 1: INIT** - Load reference files (already done)
2. **STAGE 2: INVENTORY** - Analyze ftm_schema.md
3. **STAGE 3: PLANNING** - Multiple DATA_SOURCEs? How to handle relationships?
4. **STAGE 4: MAPPING** - Map each FTM property to Senzing features
5. **STAGE 5: OUTPUTS** - Generate watchlist mapper

## Expected Outcomes

**Input:**
- ftm.jsonl (70 entities)

**Output:**
- Senzing JSONL with all entities and relationships mapped
- May need separate handling for relationship records
- International names preserved and searchable

## Validation

After mapping, you should see:
- ✅ 70 records mapped (or more if relationships become separate records)
- ✅ All person/company features recognized
- ✅ Sanction data preserved as payload
- ✅ Relationships properly encoded

{{% notice tip %}}
**Start Simple:** Map just the Person and Company entities first. Add relationships as a second step.
{{% /notice %}}

{{% notice info %}}
**Complete Solution Available:** Check `solutions/watchlist/` for reference if you get stuck.
{{% /notice %}}

{{% notice warning %}}
**PLACEHOLDER:** Detailed step-by-step instructions will be added based on demonstration video. This is an advanced exercise - attempt only after completing Module 4 successfully.
{{% /notice %}}

Ready for the challenge?
