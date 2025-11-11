---
title: "The Senzing Entity Model"
chapter: false
weight: 31
---

## Understanding Senzing's Data Format

Senzing uses a standardized JSON format for entity resolution. Each record represents either a **PERSON** or **ORGANIZATION** entity and contains structured information that Senzing uses to find matches and relationships across your data.

The key distinction to understand is **Features vs Payload**:

- **Features** - Attributes used for entity matching and resolution (NAME, ADDRESS, PHONE, EMAIL, DATE_OF_BIRTH, identifiers like SSN or PASSPORT). These go in a `FEATURES` array within your JSON record.
- **Payload** - Additional data you want to store but not use for matching (account balances, customer tiers, transaction dates). These are placed at the root level of the JSON record.

Senzing recognizes dozens of standard features with specific attribute names. For example, a NAME feature includes `NAME_FIRST`, `NAME_LAST`, and optionally `NAME_MIDDLE`, `NAME_PREFIX`, `NAME_SUFFIX`. Each feature type has its own set of expected attributes.

## What You Need to Know

Before mapping data, you should understand:

1. **Entity Types** - When to use `RECORD_TYPE: "PERSON"` vs `"ORGANIZATION"`
2. **Common Features** - NAME, ADDRESS, PHONE, EMAIL, DATE_OF_BIRTH, and standard identifiers
3. **Identifier Types** - SSN, DRIVERS_LICENSE, PASSPORT, NATIONAL_ID and when to use each
4. **Feature Structure** - How attributes nest within features
5. **The DATA_SOURCE Concept** - Every record needs a DATA_SOURCE value identifying where it came from

{{% notice tip %}}
**Don't try to memorize everything!** The AI mapping assistant will guide you through the specifications. This section is just to give you the mental model before you start.
{{% /notice %}}

## Reference Materials

For complete details on Senzing's entity format, see:

- **Full Entity Specification**: `workshop/senzing/reference/senzing_entity_specification.md` (2100+ lines covering every feature type)
- **Mapping Examples**: `workshop/senzing/reference/senzing_mapping_examples.md` (real-world examples of common mapping patterns)
- **Identifier Crosswalk**: `workshop/senzing/reference/identifier_crosswalk.json` (canonical identifier types and aliases)

You'll work with these files when using the AI mapping assistant in Module 4.

## Example Senzing Record

Here's what a complete Senzing record looks like:

```json
{
  "DATA_SOURCE": "CUSTOMERS",
  "RECORD_ID": "1001",
  "RECORD_TYPE": "PERSON",
  "PRIMARY_NAME_LAST": "Smith",
  "PRIMARY_NAME_FIRST": "John",
  "DATE_OF_BIRTH": "1985-03-15",
  "ADDR_LINE1": "123 Main Street",
  "ADDR_CITY": "Springfield",
  "ADDR_STATE": "IL",
  "ADDR_POSTAL_CODE": "62701",
  "PHONE_NUMBER": "555-1234",
  "EMAIL_ADDRESS": "john.smith@email.com",
  "SSN_NUMBER": "123-45-6789",
  "CUSTOMER_SINCE_DATE": "2020-01-15",
  "ACCOUNT_STATUS": "ACTIVE"
}
```

Notice:
- Features are at the root level using `PRIMARY_` prefix (this is the "flattened" format we'll use)
- Payload attributes (`CUSTOMER_SINCE_DATE`, `ACCOUNT_STATUS`) are also at the root
- Each record has `DATA_SOURCE`, `RECORD_ID`, and `RECORD_TYPE`

Ready to see the data you'll be mapping?
