---
title: "Introduction"
chapter: true
weight: 1
---

# Module 1: Introduction

Welcome to Module 1! This brief introduction will set the context for the workshop and explain the data mapping challenge you'll solve.

## The Data Mapping Challenge

Data mapping is the process of translating data from a source schema to a target schema. In this workshop:

- **Source Schema:** Your organization's data (customer records, watchlist data, etc.)
- **Target Schema:** Senzing's entity resolution format
- **The Challenge:** Understanding how your source attributes map to Senzing's standardized format

### Why is Data Mapping Critical?

Entity resolution can only work when your data is in the right format. Senzing uses standardized attributes like `NAME_FIRST`, `NAME_LAST`, `ADDR_LINE1`, etc. to identify and link entities. Your source data might use different field names like `customer_name`, `address`, or completely different structures.

**Traditional Approach:**
Manually analyzing fields, writing custom code, debugging issues, and updating documentation took days or weeks for each data source.

**Modern AI-Assisted Approach:**
With AI assistance and the Senzing Mapping Assistant workflow, you can:
- Automate schema analysis
- Get guided decisions on field mappings
- Generate production-ready code
- Validate output automatically
- Complete mappings in hours instead of days

## Real-World Impact

### The Customer Data Challenge

In this workshop, you'll work with a realistic customer dataset containing:
- **120 records** with both persons and organizations
- **19 fields** with varying completeness
- **Multiple identifier types** (SSN, driver's license, passport, national ID)
- **Mixed data quality** (just like real-world data)

Your goal: Transform this into validated Senzing JSON format that can identify:
- Duplicate customers with similar names and addresses
- Same person with multiple identifiers
- Organizations vs individuals
- Relationships between entities

### What Makes This Different?

This isn't just a coding exercise. You'll learn a **repeatable workflow** that combines:
- AI assistance for speed and accuracy
- Human decision-making for business context
- Professional validation tools for quality assurance
- Complete documentation for maintainability

## Workshop Flow

Here's how the modules build on each other:

1. **Module 2: Setup** - Get your tools ready (AWS environment, Amazon Q)
2. **Module 3: Understanding** - Learn the Senzing model and workflow
3. **Module 4: Hands-On** - Map 120 customer records with AI assistance ⭐
4. **Module 5: Validation** - Load data and see entity resolution in action
5. **Module 6: Bonus** - Challenge: Map complex watchlist data (optional)
6. **Module 7: Cleanup** - Wrap up and explore next steps

{{% notice tip %}}
**Module 4 is the heart of this workshop.** Modules 1-3 prepare you for it, and Module 5 validates your work. Take your time to understand the concepts before diving into hands-on mapping.
{{% /notice %}}

## What You'll Learn

By completing this workshop, you'll understand:

**Technical Skills:**
- How to use AI for structured, validated workflows (not just code generation)
- The Senzing entity resolution data model
- Difference between Features (for matching) and Payload (operational data)
- Professional validation techniques

**Practical Knowledge:**
- When to use which Senzing attributes
- How to handle mixed entity types (persons and organizations)
- Common mapping pitfalls and how to avoid them
- How to iterate and refine mappings based on validation feedback

**Process Expertise:**
- The 5-stage Senzing Mapping Assistant workflow
- How to validate mappings before production use
- Documentation practices for maintainable mappings
- How to apply this workflow to your own data

## Ready to Begin?

Now that you understand the challenge and what you'll accomplish, let's set up your environment!

**Next Step:** [Module 2: Setup and Configuration](../2_setup_configuration)
