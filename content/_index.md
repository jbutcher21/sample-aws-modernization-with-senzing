---
title: "AI-Assisted Data Mapping with Senzing"
chapter: true
weight: 1
---

# AI-Assisted Data Mapping with Senzing
<br>
![Senzing Logo](/images/senzing_logo.png)
<br>

## Overview

Welcome to the AI-Assisted Data Mapping with Senzing workshop! In this hands-on workshop, you'll learn how to leverage AI tools like Amazon Q Developer to map your data into Senzing's entity resolution format using a structured, repeatable workflow.

**About Senzing:**
Senzing provides real-time AI for entity resolution, helping organizations accurately identify and link records across disparate data sources. This workshop focuses on one of the most critical steps: mapping your source data to Senzing's format using modern AI-assisted techniques.

![What is Entity Resolution?](/images/entity_resolution_overview.png)

## Learning Objectives

By completing this workshop, you will be able to:

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
