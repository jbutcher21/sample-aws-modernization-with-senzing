---
title: "Step 2: Create Schema"
weight: 52
---

## Provide or Create the Schema

### Overview

Document the schema for the watchlist JSON data. The schema generator can help analyze the FTM format and create a schema document.

## Using the Schema Generator

**TODO:** Instructions for running the schema generator will go here.

Placeholder for:
- Running `sz_schema_generator.py` on the watchlist JSONL
- Reviewing the generated schema output
- Understanding nested field structures
- Noting FTM-specific attributes
- Saving the schema for reference

**Command:**
```bash
python3 ~/workshop/senzing/tools/sz_schema_generator.py \
  ~/workshop/workspace/watchlist/watchlist.jsonl
```

**Expected output:**
- Markdown-formatted schema document
- Field names, data types, and sample values
- Nested structure documentation
- Statistics on field population

**What you should see:**

![Step 2 - Generate Watchlist Schema](/images/exercise2/step2_schema_placeholder.png)

{{% notice tip %}}
JSON schemas are more complex than CSV. Pay attention to nested structures and arrays.
{{% /notice %}}

{{% notice info %}}
**Checkpoint:** You should have a schema document describing the watchlist data structure.
{{% /notice %}}
