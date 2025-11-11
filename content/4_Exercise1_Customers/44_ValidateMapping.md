---
title: "Step 4: Validate Mapping"
weight: 44
---

## Validate the Mapping with JSON Analyzer

### Overview

Before loading data into Senzing, validate that your mapping produces correct Senzing JSON format. Use the JSON analyzer tool to verify the mapped output.

## Run the JSON Analyzer

**Command to use:**
```bash
TODO: Placeholder command for analyzing the mapped customer JSON
```

**What you should see:**

![Step 4 - JSON Analyzer Output](/images/exercise1/step4_json_analyzer_placeholder.png)

## Interpret the Results

**TODO:** Instructions for interpreting analyzer output will go here.

Placeholder for:
- Understanding color-coded output (GREEN=recognized features, YELLOW=payload, RED=errors)
- Verifying all required fields are present
- Checking for unregistered data sources
- Identifying sparse fields
- Confirming feature mappings are correct

**Expected results:**
- All Senzing features should be GREEN
- DATA_SOURCE should be recognized
- No RED errors
- Payload fields in YELLOW (expected)

{{% notice warning %}}
If you see RED errors, fix them before proceeding to data loading.
{{% /notice %}}

{{% notice info %}}
**Checkpoint:** Your mapped data should pass validation with no errors.
{{% /notice %}}
