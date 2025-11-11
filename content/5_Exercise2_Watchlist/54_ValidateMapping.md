---
title: "Step 4: Validate Mapping"
weight: 54
---

## Validate the Mapping with JSON Analyzer

### Overview

Validate that your watchlist mapping produces correct Senzing JSON format. Use the JSON analyzer tool to verify the mapped output.

## Run the JSON Analyzer

**Command to use:**
```bash
TODO: Placeholder command for analyzing the mapped watchlist JSON
```

**What you should see:**

![Step 4 - JSON Analyzer Output](/images/exercise2/step4_json_analyzer_placeholder.png)

## Interpret the Results

**TODO:** Instructions for interpreting analyzer output will go here.

Placeholder for:
- Understanding color-coded output (GREEN=recognized features, YELLOW=payload, RED=errors)
- Verifying all required fields are present
- Checking for unregistered data sources
- Validating international name handling
- Confirming relationship mappings are correct

**Expected results:**
- All Senzing features should be GREEN
- DATA_SOURCE should be recognized
- No RED errors
- Payload fields in YELLOW (expected)
- International identifiers properly mapped

{{% notice warning %}}
If you see RED errors, fix them before proceeding to data loading.
{{% /notice %}}

{{% notice info %}}
**Checkpoint:** Your mapped watchlist data should pass validation with no errors.
{{% /notice %}}
