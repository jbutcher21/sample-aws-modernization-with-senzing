+++
title = "Stage 3: PLANNING"
weight = 433
+++

## Stage 3: PLANNING - High-Level Strategy

The AI automatically moves to planning and presents a high-level mapping strategy.

![Customer Planning 1](/images/exercise1/8-planning1.png)
![Customer Planning 2](/images/exercise1/8-planning2.png)

### The Mapping Strategy

**STAGE 3: PLANNING - High-Level Approach**

The AI will present its strategy:

**Master Entity: Customer Records**
- Entity represents both persons and organizations
- Source contains 114 individuals + 6 companies

**DATA_SOURCE Code:**
- Proposed name: **CUSTOMERS**
- Represents the source system for these records
- Must be uppercase per Senzing convention

**Entity Logic:**
- **customer_type** field controls RECORD_TYPE
  - "I" (Individual) → RECORD_TYPE: PERSON
  - "C" (Company) → RECORD_TYPE: ORGANIZATION
- Conditional mapping based on entity type

**Mapping Approach:**
- **Single-pass processing** - One mapper handles both types
- **Conditional field mapping:**
  - PERSON records: customer_name → NAME_FULL (parsed)
  - ORGANIZATION records: customer_name → NAME_ORG (unparsed)

**Special Handling: Dynamic Identifiers**
The AI identifies the id_type/id_number/id_country pattern and plans to map:
- **PASSPORT** → PASSPORT_NUMBER + PASSPORT_COUNTRY
- **DRIVERS_LICENSE** → DRIVERS_LICENSE_NUMBER + DRIVERS_LICENSE_STATE
- **SSN** → SSN_NUMBER
- **NATIONAL_ID** → NATIONAL_ID_NUMBER + NATIONAL_ID_COUNTRY

The assistant confirms: **"✅ STAGE 3 COMPLETE - Strategy defined"**

**Important:** Remember, your response may not match this exactly, as the AI's output can vary.

### Ask Questions!

This is your opportunity to clarify any strategy decisions before field mapping begins.

You probably see something about `dynamic identifiers` ...

**Ask Amazon Q:** `What are dynamic identifiers?`

### Give Direction!

If you don't like the data source it assigned ...

**Tell Amazon Q:** `Call the data source CUSTOMER`

If you want to only load person records ...

**Tell Amazon Q:** `Filter out the companies`

### Advance to Mapping

When you understand the strategy:

**Tell Amazon Q:** `yes`

::alert[**LEARNING OPPORTUNITY:** The more questions you ask the more you will learn!]{type="warning"}

::alert[**Checkpoint:** You and Q should agree on the high level strategy for mapping customers.]{type="warning"}
