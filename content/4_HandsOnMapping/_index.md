---
title: "Hands-On: Map Customer Data with AI"
chapter: true
weight: 4
---

# Hands-On: Map Customer Data with AI

## Overview

In this module, you'll use AI (Amazon Q Developer) to map the customer dataset to Senzing format using the Senzing Mapping Assistant workflow. This is a fully guided, hands-on exercise with complete validation at every step.

## What You'll Do

1. **Load the Mapping Assistant** - Initialize the AI-powered mapping workflow
2. **Analyze Source Schema** - Let AI inventory all fields in customers.csv
3. **Plan the Mapping** - Determine DATA_SOURCE and entity types
4. **Map Each Field** - Decide which fields are Features vs Payload
5. **Generate Outputs** - Create mapper code, documentation, and mapped data
6. **Validate Results** - Use Senzing tools to verify the mapping

## Workshop Materials

All materials are in your Cloud9 environment under `workshop/`:

**Source Data:**
- `workspace/customers/customers.csv` - 120 customer records (114 persons, 6 organizations)
- `workspace/solutions/customers/customers_schema.md` - Pre-generated schema analysis

**Senzing Resources:**
- `senzing/prompts/senzing_mapping_assistant.md` - The AI mapping workflow
- `senzing/reference/` - Entity specification, examples, crosswalks, linter
- `senzing/tools/` - Schema generator, JSON analyzer

**Complete Solution (for reference):**
- `solutions/customers/` - All completed mapping files

## The Mapping Workflow

You'll follow the **Senzing Mapping Assistant v4** 5-stage process:

1. **STAGE 1: INIT** - Load reference files and verify tools
2. **STAGE 2: INVENTORY** - Extract all source fields
3. **STAGE 3: PLANNING** - Identify entities and DATA_SOURCE codes
4. **STAGE 4: MAPPING** - Map each field with AI guidance
5. **STAGE 5: OUTPUTS** - Generate mapper script and documentation

{{% notice tip %}}
**AI-Assisted but Human-Driven:** The AI guides you through decisions, but YOU make the final calls. When the AI asks questions, provide clear answers based on your understanding of the data.
{{% /notice %}}

{{% notice info %}}
**Video Demonstration:** A complete walkthrough video shows the entire mapping process from start to finish, including all prompts, decisions, and validation steps.
{{% /notice %}}

## Key Learning Objectives

By the end of this module, you will:

- ✅ Understand the 5-stage AI-assisted mapping workflow
- ✅ Know how to disposition fields as Features vs Payload
- ✅ Learn to resolve naming conflicts (e.g., CUSTOMER_SINCE_DATE)
- ✅ Generate production-ready mapper code
- ✅ Validate mapped data with Senzing tools
- ✅ Interpret sz_json_analyzer output

## Expected Outcomes

**Input:**
- customers.csv (120 records, 19 fields)

**Output:**
- customers_senzing.jsonl (120 records, fully validated)
- customers_mapper.py (Python mapper)
- Complete mapping documentation

**Validation:**
- ✅ Linter passes (0 errors)
- ✅ All features recognized by Senzing
- ✅ Payload attributes properly separated

## Ready?

Let's start mapping!
