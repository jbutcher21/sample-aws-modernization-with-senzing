---
title: "Load and Validate Mapped Data"
chapter: true
weight: 5
---

# Load and Validate Mapped Data

## Overview

Now that you've successfully mapped your customer data to Senzing format, it's time to load it into Senzing and see entity resolution in action! This module shows you how to register your data source, load the mapped data, and explore the resolved entities.

## What You'll Do

1. **Register DATA_SOURCE** - Add "CUSTOMERS" to Senzing configuration
2. **Load Mapped Data** - Import customers_senzing.jsonl into Senzing
3. **Take a Snapshot** - Create a point-in-time view of resolved entities
4. **Explore Results** - See which records resolved into entities
5. **Analyze Matches** - Understand why entities matched

## Prerequisites

Before starting this module, you should have:

- ✅ Completed Module 4 (Customer mapping)
- ✅ File: `workspace/customers/customers_senzing.jsonl` (120 records)
- ✅ Validation: Passed linter and sz_json_analyzer

{{% notice info %}}
**Catch-Up Option:** If you didn't complete Module 4, copy the solution:
```bash
cp solutions/customers/customers_senzing.jsonl workspace/customers/
```
{{% /notice %}}

## The Senzing Tools

You'll use these Senzing SDK tools:

| Tool | Purpose | What It Does |
|------|---------|--------------|
| `sz_configtool` | Configuration | Add/modify data sources and features |
| `sz_file_loader` | Data Loading | Import JSONL files into Senzing |
| `sz_snapshot` | Export | Create JSON snapshot of resolved entities |
| `sz_explorer` | Exploration | Interactive UI to browse entities |

## Expected Results

After loading 120 customer records, you should see:

- **Entity Count**: Fewer than 120 (some duplicates should resolve)
- **Key Resolutions**:
  - The 3 "Mooney, Susan" records → Should resolve to 1-2 entities
  - Records with matching identifiers → Should resolve
  - Records with similar names + addresses → May resolve

## Learning Objectives

By the end of this module, you will:

- ✅ Understand how to configure Senzing for new data sources
- ✅ Know how to load mapped data into Senzing
- ✅ Be able to explore resolved entities
- ✅ Understand entity resolution match rules
- ✅ Interpret why records matched or didn't match

## Validation Checkpoints

**Checkpoint 1: Configuration**
- ✅ DATA_SOURCE "CUSTOMERS" registered
- ✅ No configuration errors

**Checkpoint 2: Loading**
- ✅ 120 records loaded successfully
- ✅ No load errors reported

**Checkpoint 3: Resolution**
- ✅ Entities created (< 120)
- ✅ Expected duplicates resolved
- ✅ Match keys visible in snapshot

{{% notice tip %}}
**Using AI:** You can ask Amazon Q Developer to help you run these commands and interpret the results. The AI can explain what the output means and help troubleshoot any issues.
{{% /notice %}}

{{% notice warning %}}
**PLACEHOLDER:** Detailed step-by-step instructions will be added based on demonstration video, including:
- Exact commands to run
- Expected outputs at each step
- How to interpret results
- Troubleshooting common issues
{{% /notice %}}

Ready to load your data and see entity resolution in action?
