---
title: "Step 2: Create Schema"
weight: 42
---

## Provide or Create the Schema

### Overview

Now that you've examined the data, you need to document its schema. You can use the Senzing schema generator tool to automatically analyze the CSV and create a schema document.

## Using the Schema Generator

**TODO:** Instructions for running the schema generator will go here.

Placeholder for:
- Running `sz_schema_generator.py` on the customers CSV
- Reviewing the generated schema output
- Understanding field types and sample values
- Saving the schema for reference

**Command:**
```bash
python3 ~/workshop/senzing/tools/sz_schema_generator.py \
  ~/workshop/workspace/customers/customers.csv
```

**Expected output:**
- Markdown-formatted schema document
- Field names, data types, and sample values
- Statistics on field population

{{% notice tip %}}
The schema document helps you and the AI understand the data structure during the mapping process.
{{% /notice %}}

{{% notice info %}}
**Checkpoint:** You should have a schema document describing all fields in the customer data.
{{% /notice %}}
