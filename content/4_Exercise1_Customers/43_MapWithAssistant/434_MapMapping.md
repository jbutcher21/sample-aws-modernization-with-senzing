---
title: "Stage 4: MAPPING"
weight: 434
---

## Stage 4: MAPPING - Field-by-Field Decisions

This is the core of the mapping process. The AI will present a complete field disposition table with confidence scores.

![Customer Mapping 1](/images/exercise1/9-mapping1.png)
![Customer Mapping 2](/images/exercise1/9-mapping2.png)

### The Field Disposition Table

This is the most critical stage of the mapping process. Take your time here to understand each decision the AI makes.

{{% notice tip %}}
**Learning Opportunity:** This stage offers the best opportunity to understand entity resolution concepts. Don't rush through - ask questions about anything unclear!
{{% /notice %}}

### Ask Questions About the Table Structure

The mapping table may look confusing at first. Ask the AI to explain the key elements:

**Ask Amazon Q:** `What does the REF column mean?`

**Ask Amazon Q:** `What does the confidence score indicate?`

**Ask Amazon Q:** `What is RECORD_TYPE and why does it matter?`

**Ask Amazon Q:** `Explain the logic for NAME_FULL vs NAME_ORG`

The AI will explain how it uses the Senzing specification to make each decision.

### Review Mapping Decisions Carefully

While the AI gets many mappings correct, it can make mistakes based on limited context from your schema.

**Common issues to watch for:**

**Address Mapping:**
- The AI might map `address` to `ADDR_FULL` based on sample values in your schema
- If your address field contains only street addresses, `ADDR_LINE1` may be more appropriate
- Example correction: **Tell Amazon Q:** `Change the address mapping from ADDR_FULL to ADDR_LINE1`

**Name Parsing:**
- The AI may suggest parsing `customer_name` into `NAME_FIRST` and `NAME_LAST`
- This works well if your data is consistent, but can fail on varied formats
- If you prefer unparsed names: **Tell Amazon Q:** `Map customer_name to NAME_FULL without parsing`

**Identifier Types:**

If your data has dynamic identifier patterns (like `id_type` and `id_number` fields), verify the AI mapped all possible type codes. The schema generator only shows the most common values.

**Ask Amazon Q:** `What are all the possible values for id_type in the source data?`

Once you have the complete list, verify each code maps to the correct Senzing feature:
- `SSN` → SSN_NUMBER
- `DL` → DRIVERS_LICENSE_NUMBER
- `PASSPORT` → PASSPORT_NUMBER
- `NATIONAL_ID` → NATIONAL_ID_NUMBER

If the AI missed any codes: **Tell Amazon Q:** `Add mapping for id_type='CEDULA' to NATIONAL_ID_NUMBER`

{{% notice note %}}
**Don't Worry About Perfection:** Additional validation steps will catch issues during the linter stage. Focus on understanding the major decisions and correcting obvious problems. This workflow is designed to help you iterate quickly to a working result - which is the only proof that truly matters.
{{% /notice %}}

### Review and Approve

Once you've asked your questions and made any corrections:

**Tell Amazon Q:** `The mappings look good, proceed to validation`

### Linter Validation

The AI will generate sample JSON records and run the Senzing linter to validate the mapping structure. The AI can usually self-correct any errors, but may ask for clarification.

{{% notice tip %}}
**You Can Intervene:** If the AI is doing something you don't understand, press Escape and ask questions before it continues.
{{% /notice %}}

**Common validation issue - REGISTRATION_DATE:**

If your source data has a field called `registration_date`, the linter may flag it because Senzing has a reserved feature called REGISTRATION_DATE (for legal business incorporation dates).

If this happens:

**Ask Amazon Q:** `Does our customer registration date qualify as the Senzing REGISTRATION_DATE feature?`

The AI will explain that customer registration dates don't match the Senzing feature definition. The solution is to keep it as payload and rename it:

**Tell Amazon Q:** `Rename registration_date to CUSTOMER_SINCE_DATE in the payload`

When validation succeeds, you'll see confirmation:

![Linter validation successful](/images/exercise1/10-linter-pass.png)

The assistant confirms: **"✅ STAGE 4 COMPLETE - Mapping validated"**

### Advance to Outputs

When the linter validates successfully:

**Tell Amazon Q:** `yes`

{{% notice info %}}
**Checkpoint:** Q should present a complete field disposition table with confidence scores, generate valid sample JSON, and pass linter validation before moving to OUTPUTS.
{{% /notice %}}
