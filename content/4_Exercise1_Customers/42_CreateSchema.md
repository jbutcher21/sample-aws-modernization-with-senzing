---
title: "Step 2: Generate Schema"
weight: 42
---

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

{{% notice tip %}}
**Pro Tip:** For complex schemas the tool cannot handle, locate the official schema documentation or ask AI to help extract schema information from documentation.
{{% /notice %}}

## Generate the Schema with Amazon Q

**Ask Amazon Q to generate the schema:**

Open Amazon Q Developer (click the Q icon in the left sidebar)

**Tell Amazon Q:** `Generate a schema for the customer CSV`

![Amazon Q generating schema - request approval](/images/exercise1/2-gen-schema1.png)

{{% notice warning %}}
**Security Note:** Notice that Q asks for your approval before running the schema generator. This is an important security feature - never give tools blanket access to run commands without review. Always verify what actions AI wants to take before approving.
{{% /notice %}}

**Review Q's response:**

![Amazon Q schema generation response](/images/exercise1/2-gen-schema2.png)

Q Developer will run the schema generator tool and create a `customer_schema.md` file in your workspace.

## Review the Generated Schema

**Open the schema file:**

1. In your IDE file explorer, navigate to `workshop/workspace/customers/`
2. Open `customer_schema.md`

![Customer schema document](/images/exercise1/2-gen-schema3.png)

Review the schema to understand:
- What fields are available
- Which fields have high population rates (good for matching)
- What the data values look like

This schema document will help guide the AI during the mapping process.

## Fallback: Use the Pre-Generated Schema

If you encounter issues generating the schema, a pre-generated version is available in the solutions folder:

`workshop/solutions/customers/customer_schema.md`

{{% notice info %}}
**Checkpoint:** You should have a `customer_schema.md` file that documents all fields, data types, and sample values from the customer CSV.
{{% /notice %}}
