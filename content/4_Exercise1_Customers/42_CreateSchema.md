+++
title = "Step 2: Generate Schema"
weight = 42
+++

## First: Examine Your Source Data

Before generating the schema, you need to understand your data structure and business goals.

**Open the customer CSV file:**

In your IDE file explorer (left sidebar), navigate to:
1. Navigate to the `workshop/workspace/customers` directory
2. Expand the folder to see its contents
3. **Double-click** `customers.csv` to open it in your IDE

![Customer CSV file open in IDE](/images/exercise1/1-customer.png)

**Review the data structure:**
   - Scroll through the first 10-20 rows
   - Note the column headers
   - Observe data patterns and completeness
   - Look for different customer types (Individual vs Company)

4. **Define your business objective:**
   - Are you trying to find duplicate customers?
   - Will you match this against other datasets?
   - What constitutes a "match" for your use case?

**Remember:** You guide the AI - understanding your data and goals ensures better mapping results.

## Generate a Data Schema

Now that you've examined the customer data, you need to document its structure. A schema document provides essential information about field types, population rates, and sample values - critical details for accurate mapping.

## Why Generate a Schema?

When mapping data, AI needs to understand both the source and target schemas. However, you shouldn't upload entire data files to AI because:

1. **Privacy concerns** - Files may contain sensitive customer information
2. **Context limits** - AI models have limited context windows and cannot process large files
3. **Accuracy** - AI can infer schema from sample rows, but this is error-prone

Instead, you'll use the Senzing schema generator tool to create a comprehensive schema document that includes:
- Field names and data types
- Population percentages (how often fields contain values)
- Sample values and ranges
- Field statistics

::alert[**Pro Tip:** For complex schemas the tool cannot handle, locate the official schema documentation or ask AI to help extract schema information from documentation.]{type="warning"}

## Generate the Schema with Amazon Q

**Ask Amazon Q to generate the schema:**

Open Amazon Q Developer (click the Q icon in the left sidebar)

**Tell Amazon Q:** `Generate a schema for the customer CSV`

![Request approval](/images/exercise1/5-security-example.png)

::alert[**Security Note:** Notice that Q asks for your approval before running the schema generator. This is an important security feature - never give tools blanket access to run commands without review. Always verify what actions AI wants to take before approving.]{type="warning"}

Q Developer will run the schema generator tool and create a `customer_schema.md` file in your workspace.

**Review Q's response:**

Q Developer will run the schema generator tool and create a `customer_schema.md` file in your workspace.

![Amazon Q schema generation response](/images/exercise1/5-customer-schema.png)

## Review the Generated Schema

**Compare the actual schema with the AI summary:**

1. In your IDE file explorer, navigate to `workshop/workspace/customers/`
2. Open `customer_schema.md`
3. Compare the actual schema content with the AI summary below

Does the summary match what you see in the file?

### Schema Analysis: 120 Records, 19 Fields

The schema generator will show you detailed statistics for your customer data:

**Core Identity (100% population):**
- **customer_id** - Unique record identifier
- **customer_name** - Full customer names
- **customer_type** - "I" (Individual/Person) or "C" (Company/Organization)

**Demographics:**
- **gender** (17%) - Gender information (sparse)
- **dob** (53%) - Date of birth (moderate coverage)

**Location Information (varying coverage):**
- **address** (61%) - Street addresses
- **city, state, zip_code, country** - Address components

**Contact Information:**
- **phone** (18%) - Phone numbers (sparse)
- **email** (38%) - Email addresses (moderate)

**Identifiers (30% population):**
The schema shows a **dynamic identifier pattern** with three related fields:
- **id_type** - Type code (PASSPORT, DRIVERS_LICENSE, SSN, NATIONAL_ID)
- **id_number** - The identifier value
- **id_country** - Issuing country

This pattern means you'll need special handling to map these to the correct Senzing features.

**Business/Operational Data:**
- **registration_date** (83%) - When customer joined
- **account_status** (83%) - Active/Inactive status
- **account_balance** (75%) - Current balance
- **customer_tier** - Customer classification

### Dataset Composition

**Entity Mix:**
- **114 Person records** (customer_type = "I")
- **6 Organization records** (customer_type = "C")
- **Total: 120 records**

This mix means your mapper needs to handle both PERSON and ORGANIZATION entity types, mapping fields conditionally based on customer_type.

### Data Quality Observations

- **High-value matching fields:** customer_name (100%), dob (53%), address (61%)
- **Sparse fields:** gender (17%), phone (18%) - less reliable for matching
- **Good identifier coverage:** 30% have government IDs
- **Strong operational data:** 75-83% coverage on business fields

This schema document will guide the AI during mapping to make informed decisions about which fields to use for entity resolution.

## Fallback: Use the Pre-Generated Schema

If you encounter issues generating the schema, a pre-generated version is available in the solutions folder:

`workshop/solutions/customers/customer_schema.md`

::alert[**Checkpoint:** You should have a `customer_schema.md` file that documents all fields, data types, and sample values from the customer CSV.]{type="warning"}
