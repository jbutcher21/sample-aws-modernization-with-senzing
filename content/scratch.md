---
title: "Introduction"
chapter: true
weight: 1
---

# Introduction

Overview What is entity resolutiuon?

shows the entity resolution image here.

# The data mapping challenge:

Data mapping is the process of translating data from a source schema to a target schema. 

- **Source Schema:** Your organization's data (customer records, watchlist data, etc.)
- **Target Schema:** Senzing's entity resolution format
- **The Challenge:** Understanding how your source attributes map to Senzing's standardized format


# Overview

Specifically, you will be able to:

- Understand the Senzing entity resolution data model and requirements
- Use AI tools (Amazon Q Developer) to assist with data mapping workflows
- Analyze your source data and what it contains
- Apply best practices for production data mapping projects
- Create mapping logic that transforms source data to Senzing format
- Load mapped data into Senzing and validate the results

## Prerequisites

- Basic understanding of data formats (CSV, JSON)
- Basic Python knowledge (helpful but not required)
- Basic understanding of AWS core services
- AWS account with appropriate permissions (provided in AWS-led event)
- Familiarity with using an IDE (preferably code-server)
- Familiarity with using an AI assistant
- Familiarity with command-line interfaces

## What You'll Build

Throughout this workshop, you will create a complete, production-ready data mapping pipeline:

- **Schema analysis documents** profiling your source data
- **Mapping specifications** documenting field-by-field decisions
- **Python mapper code** that transforms CSV to Senzing JSON format
- **Validated entity data** ready to load into Senzing
- **Entity resolution results** showing how Senzing identifies duplicates

## Workshop Structure

This workshop is divided into the following modules:

| Module | Duration | Description |
|--------|----------|-------------|
| **Module 1: Introduction** | 10 minutes | Workshop overview and learning objectives |
| **Module 2: Setup & Configuration** | 15 minutes | Access your development environment and configure Amazon Q |
| **Module 3: Understanding Senzing Mapping** | 30 minutes | Learn the Senzing data model and mapping workflow |
| **Module 4: Hands-On - Map Customer Data** | 60 minutes | Use AI to map customer records to Senzing format |
| **Module 5: Load and Validate** | 30 minutes | Load your mapped data and see entity resolution in action |
| **Module 6: Bonus - Watchlist Mapping** | 45 minutes | *Optional:* Map complex international watchlist data |
| **Module 7: Cleanup and Next Steps** | 10 minutes | Clean up resources and explore what's next |

**Total Time: Approximately 2.5-3 hours** (core modules 1-5)

## Workshop Modules

### Module 1: Introduction
Get oriented with the workshop goals, structure, and the data mapping challenge you'll solve.

### Module 2: Setup and Configuration
Access your development environment and authenticate with Amazon Q Developer for both the IDE and CLI.

### Module 3: Understanding Senzing Mapping
Learn the Senzing entity resolution data model, the difference between Features and Payload attributes, and the 5-stage mapping workflow.

### Module 4: Hands-On Customer Mapping ⭐ **Core Module**
Apply what you learned: analyze customer data, make mapping decisions with AI guidance, generate mapper code, and validate your output.

### Module 5: Load and Validate
See your mapping in action by loading data into Senzing and exploring entity resolution results.

### Module 6: Bonus - Watchlist Mapping (Optional)
Challenge yourself with more complex data including nested structures, international names, and entity relationships.

### Module 7: Cleanup and Next Steps
Clean up your AWS resources and learn how to apply these skills to your own data.

## Getting Started

Ready to begin? Here's what happens next:

1. **Read Module 1** to understand the context and learning objectives
2. **Complete Module 2** to set up your development environment
3. **Learn the concepts** in Module 3 before diving into hands-on work
4. **Map customer data** in Module 4 using AI assistance
5. **Validate your work** in Module 5 by loading into Senzing

{{% notice tip %}}
**Self-Paced Approach:** This workshop is designed for self-paced learning. Take your time, use the validation checkpoints, and reference the complete solutions if you get stuck.
{{% /notice %}}

## Workshop Conventions

Throughout this workshop, you'll encounter various visual elements to help guide your learning:

{{% notice tip %}}
**Tips** provide helpful suggestions and best practices.
{{% /notice %}}

{{% notice info %}}
**Info boxes** highlight important information or context.
{{% /notice %}}

{{% notice warning %}}
**Warnings** alert you to common pitfalls or important considerations.
{{% /notice %}}

**Code Blocks:**
```bash
# Command-line instructions look like this
python3 mapper.py input.csv -o output.jsonl
```

**Validation Checkpoints:**
✅ Green checkmarks indicate validation steps to confirm your progress

## Support and Resources

### Workshop Support

**During Instructor-Led Events:**
- Ask your instructor or workshop facilitators
- Use the event chat or Q&A features

**For Self-Paced Learners:**
- Review the complete solutions provided in each module
- Check the troubleshooting sections
- Consult the Senzing documentation links below

### Senzing Resources

- **Senzing Documentation:** [https://senzing.com/docs/](https://senzing.com/docs/)
- **Senzing GitHub:** [https://github.com/senzing](https://github.com/senzing)
- **Senzing Community Support:** [https://senzing.com/support/](https://senzing.com/support/)

### AWS Resources

- **Amazon Q Developer Documentation:** [https://docs.aws.amazon.com/amazonq/latest/qdeveloper-ug/](https://docs.aws.amazon.com/amazonq/latest/qdeveloper-ug/)
- **AWS Builder ID:** [https://profile.aws.amazon.com/](https://profile.aws.amazon.com/)
- **AWS Workshop Studio:** [https://workshops.aws/](https://workshops.aws/)

## Goals

By the end of this workshop, you will have:

**Practical Skills:**
- Mapped real data to Senzing format using AI assistance
- Created production-ready mapper code
- Validated your mappings with professional tools

**Deep Understanding:**
- Know the Senzing entity resolution data model
- Understand Features vs Payload attributes
- Recognize common mapping patterns and best practices

**Repeatable Process:**
- Learned the 5-stage Senzing Mapping Assistant workflow
- Can apply this workflow to any data source
- Know how to validate and iterate on your mappings

---

{{% notice warning %}}
The examples and sample code provided in this workshop are intended to be consumed as instructional content. These will help you understand how various AWS services can be architected to build a solution while demonstrating best practices along the way. These examples are not intended for use in production environments.
{{% /notice %}}

**Ready to get started? Let's begin with [Module 1: Introduction](1_moduleone)!**


after setup there should be Modules for

- Some sort of the problem with mapping and why this was built?
- Exercise Workflow
- Exercise 1 - mapping the customer file
- Exercise 2 - mapping the watchlist file
- some sort of wrap up


In each exercise we will have the same tasks (the overview will briefly describe the steps and tools)

1. Examine the source data
2. Provide or create the schema
3. Use the senzing mapping assistant to map it
4. Validate the mapping with the json analyzer
5. Load the data in Senzing
6. Take a snaphot
7. Analyze the snapshot for stats and examples
8. Review the examples with the mcp server by asking how and why questions

--------------------------------------

**Source Data (Your Format):**
- CSV with columns like: customer_id, customer_name, dob, address, email...
- May have organization-specific field names
- Mixed data quality and completeness

**Target Data (Senzing Format):**
- JSON with standardized features: NAME, DATE_OF_BIRTH, ADDRESS, EMAIL...
- Specific attribute names (NAME_FIRST, NAME_LAST, ADDR_LINE1...)
- Clear distinction between matching features and payload data

## The Challenge

Knowing which source fields map to which Senzing features, and how to transform the data correctly.

**For each source field, you must decide:**
- Should it be a Feature (used for entity matching)?
- Should it be Payload (stored but not matched)?
- Which specific Senzing attribute name is correct?
- Does the data need transformation (date formats, name parsing, etc.)?

**Example decisions:**
- Your CSV has `customer_name` - should this map to `NAME_FULL`? Or split into `NAME_FIRST` and `NAME_LAST`?
- You have `id_number` - is this an SSN? Driver's License? Passport?
- Your `registration_date` - is this legal entity registration or customer signup date? (Very different meanings!)

## Traditional Manual Approach

Without AI assistance, data mapping typically requires:

1. **Reading specifications** - Understanding hundreds of Senzing features and attributes
2. **Making decisions** - Determining appropriate mappings for each field
3. **Writing code** - Building transformation logic
4. **Manual validation** - Checking outputs meet requirements
5. **Iterative debugging** - Finding and fixing errors

**Time cost:** 3-6 days for a typical dataset with 15-20 fields

## The AI-Assisted Solution

This workshop teaches you to use the **Senzing Mapping Assistant** - a structured AI workflow that:

✅ **Reads specifications instantly** - AI loads the complete Senzing spec into context
✅ **Suggests mappings** - AI recommends appropriate features based on your data
✅ **Generates code** - AI writes the mapper automatically
✅ **Creates documentation** - Mapping decisions documented as byproduct

**Time savings:** Same work in **under an hour**

{{% notice warning %}}
**Important Caveat**: AI is your assistant, not a replacement for your judgment. YOU still need to:
- Understand what your source fields mean
- Make business decisions about what should influence matching
- Validate that AI suggestions align with your requirements
- Correct AI when it misunderstands your data
{{% /notice %}}

## What You'll Learn

In this workshop, you'll learn:
- The Senzing entity model (Features vs Payload, entity types)
- How to work with AI to make mapping decisions
- A repeatable 5-stage workflow for any dataset
- Professional validation tools to verify correctness
- How to load and analyze entity resolution results

Ready to understand Senzing's data model?


----------------------
## The 5 Stages

### STAGE 1: INIT - Load Reference Materials

You load the Senzing specifications and reference materials into the AI context. This gives the AI the knowledge it needs to guide you through mapping.

**What happens:**
- Load entity specification
- Load mapping examples
- Load validation tools
- Load identifier and usage type crosswalks

**Your role:** Copy prompts to load files into AI context

---

### STAGE 2: INVENTORY - Analyze Source Data

The AI analyzes your source data schema to understand what fields you're working with.

**What happens:**
- AI reviews pre-generated schema file
- Identifies field names, data types, population rates
- Notes patterns and potential issues

**Your role:** Provide schema file (generated by `sz_schema_generator.py`)

---

### STAGE 3: PLANNING - Identify Entities and Sources

You work with the AI to determine:
- What DATA_SOURCE value to use
- Are there multiple entity types in your data?
- Any special handling needed?

**What happens:**
- AI asks clarifying questions
- You make business decisions
- Establish mapping strategy

**Your role:** Answer questions about your data and business context

---

### STAGE 4: MAPPING - Field-by-Field Decisions

This is the core mapping work. For each source field, you and the AI determine:
- Should it be a Senzing Feature (used for matching)?
- Should it be Payload (stored but not matched)?
- Should it be ignored?
- What is the correct Senzing attribute name?

**What happens:**
- AI suggests mappings based on field names and content
- You confirm or override decisions
- Handle edge cases (e.g., dynamic identifier types)
- Decide on data transformations (date formats, name parsing)

**Your role:** Make informed decisions with AI guidance

---

### STAGE 5: OUTPUTS - Generate Code and Documentation

The AI generates production-ready deliverables:

**Outputs:**
- **Mapper specification** (markdown documentation of all decisions)
- **Python mapper** (executable code)
- **Sample output** (example mapped JSON records)
- **README** (usage instructions)

**What happens:**
- AI writes the mapper based on Stage 4 decisions
- You run the mapper
- Validate output with linting and analysis tools

**Your role:** Review generated code, run mapper, validate output

---

## Why This Workflow Works

**Structured Decision-Making**: Each stage has a clear purpose and deliverable

**Validation Gates**: You verify correctness at each stage before proceeding

**Iterative Refinement**: Easy to go back and adjust decisions

**Documentation Trail**: Complete record of why each mapping decision was made

**Production Ready**: Output includes code, documentation, and validation

{{% notice tip %}}
**This isn't just code generation** - it's AI-assisted decision-making with you in control. The AI guides you through the specifications and best practices, but YOU make the final decisions based on your understanding of the data.
{{% /notice %}}

## The Full Prompt

The complete Senzing Mapping Assistant prompt with detailed instructions for each stage is available at:

**`workshop/senzing/prompts/senzing_mapping_assistant.md`**

You'll load this prompt in Module 4 when you start the hands-on customer mapping exercise.

## What to Expect in Module 4

In the next module, you'll:
1. Load the Mapping Assistant into Amazon Q Developer
2. Work through all 5 stages for the customer dataset
3. Make real mapping decisions with AI guidance
4. Generate a working mapper
5. Validate your output with linting and analysis tools

**Estimated time**: 60 minutes for complete customer mapping

Ready to learn about the validation tools you'll use?
