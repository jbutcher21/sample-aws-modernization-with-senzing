---
title: "What You'll Learn"
chapter: false
weight: 35
---

# What You'll Learn in This Workshop

By completing this workshop, you'll gain comprehensive knowledge across three areas: technical skills, practical knowledge, and process expertise.

## Technical Skills

You'll understand:

**AI-Assisted Workflows:**
- How to use AI for structured, validated workflows (not just code generation)
- How to guide AI with proper context and reference materials
- When to accept AI suggestions vs when to override them

**Senzing Entity Resolution:**
- The Senzing entity resolution data model
- Difference between **Features** (used for matching) and **Payload** (operational data)
- How Senzing uses features to identify duplicate entities

**Validation Techniques:**
- Professional validation tools (`lint_senzing_json.py`, `sz_json_analyzer.py`)
- How to interpret validation output
- Iterative refinement based on validation feedback

## Practical Knowledge

You'll learn:

**Mapping Decisions:**
- When to use which Senzing attributes (NAME, ADDRESS, identifiers, etc.)
- How to handle mixed entity types (persons and organizations)
- Common mapping pitfalls and how to avoid them

**Data Transformations:**
- How to parse complex identifier fields
- Date format standardization
- Handling missing or incomplete data

**Real-World Challenges:**
- Working with varying data completeness
- Mapping dynamic identifier fields
- Distinguishing operational data (payload) from matching data (features)

## Process Expertise

You'll master:

**The 5-Stage Senzing Mapping Assistant Workflow:**
1. **INIT** - Loading reference materials into AI context
2. **INVENTORY** - Analyzing source data schema
3. **PLANNING** - Determining data sources and entity types
4. **MAPPING** - Making field-by-field mapping decisions
5. **OUTPUTS** - Generating code, documentation, and validated output

**Validation Practices:**
- How to validate mappings before production use
- Using linting to catch syntax errors
- Using analysis tools to verify attribute recognition
- Iterating on mappings based on validation results

**Documentation:**
- Creating mapping specifications
- Documenting business decisions
- Maintaining mapper code with clear comments

**Repeatability:**
- How to apply this workflow to your own data sources
- Adapting the process for different data formats (CSV, JSON, XML)
- Building a library of reusable mapping patterns

## What You'll Have at the End

By completing this workshop, you will have:

**Practical Deliverables:**
- ✅ Mapped real customer data to Senzing format using AI assistance
- ✅ Created production-ready mapper code
- ✅ Validated your mappings with professional tools
- ✅ Complete mapping documentation

**Deep Understanding:**
- ✅ Know the Senzing entity resolution data model
- ✅ Understand Features vs Payload attributes
- ✅ Recognize common mapping patterns and best practices

**Repeatable Process:**
- ✅ Learned the 5-stage Senzing Mapping Assistant workflow
- ✅ Can apply this workflow to any data source
- ✅ Know how to validate and iterate on your mappings

{{% notice info %}}
This workshop focuses on **mapping** - preparing data for entity resolution. Loading the mapped data into Senzing and viewing resolution results is covered in Module 5.
{{% /notice %}}

## Module-by-Module Learning Path

Here's how the workshop builds your knowledge:

**Module 1:** Workshop overview and orientation
**Module 2:** Environment setup with Amazon Q Developer and Senzing
**Module 3:** (Current) Understanding concepts and workflow
**Module 4:** Hands-on customer data mapping with AI
**Module 5:** Loading mapped data and viewing entity resolution results
**Module 6:** (Bonus) Advanced mapping with watchlist data and relationships
**Module 7:** Cleanup and next steps

Ready to dive into hands-on mapping? Continue to Module 4!
