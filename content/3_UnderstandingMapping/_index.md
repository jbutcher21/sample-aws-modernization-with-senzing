---
title: "Understanding Senzing Mapping"
chapter: true
weight: 3
---

# Understanding Senzing Mapping

## Overview

Before diving into hands-on mapping, you need to understand the Senzing data model, the tools available, and the AI-assisted workflow you'll use. This module prepares you for successful data mapping.

## What You'll Learn

In this module, you will:

1. **Understand the Senzing Entity Model** - What Senzing needs for entity resolution
2. **Explore Your Source Data** - Customer and watchlist datasets
3. **Learn the Mapping Workflow** - The 5-stage Senzing Mapping Assistant process
4. **See Validation Tools** - How to verify your mappings are correct

## The Data Mapping Challenge

Data mapping translates your organization's data format into Senzing's standardized entity resolution format:

**Source Data (Your Format):**
- CSV with columns like: customer_id, customer_name, dob, address, email...
- May have organization-specific field names
- Mixed data quality and completeness

**Target Data (Senzing Format):**
- JSON with standardized features: NAME, DATE_OF_BIRTH, ADDRESS, EMAIL...
- Specific attribute names (NAME_FIRST, NAME_LAST, ADDR_LINE1...)
- Clear distinction between matching features and payload data

**The Challenge:** Knowing which source fields map to which Senzing features, and how to transform the data correctly.

**The Solution:** AI-assisted mapping with validation at every step!

## Module Sections

This module covers four essential topics. Click through each section to learn:

1. **[The Senzing Entity Model](31_senzingentityspec)** - Understanding Features vs Payload, entity types, and Senzing's data format
2. **[Your Workshop Datasets](32_workshopdata)** - Customer data (120 records) and watchlist data (70 entities) that you'll be mapping
3. **[The 5-Stage Mapping Workflow](33_mappingworkflow)** - The Senzing Mapping Assistant process (INIT → INVENTORY → PLANNING → MAPPING → OUTPUTS)
4. **[Validation Tools](34_validationtools)** - Schema generator, JSON linter, and Senzing analyzer

**Estimated Reading Time:** 15-20 minutes

{{% notice tip %}}
**This module is mostly reading and exploration** - you won't be doing the mapping yet. Module 4 is where you'll actually map the customer data with AI assistance.
{{% /notice %}}

Ready to learn about Senzing's data model?
