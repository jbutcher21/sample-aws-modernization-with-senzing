---
title: "Stage 5: OUTPUTS"
weight: 435
---

## Stage 5: OUTPUTS - Generate Code and Docs

The AI generates three production-ready files that document and implement your mapping.

![Output code and documentation 1](/images/exercise1/11-output1.png)
![Output code and documentation 2](/images/exercise1/11-output2.png)

### The Generated Files

**STAGE 5: OUTPUTS - Generating Implementation**

The AI creates three files in `workshop/workspace/customers/`:

**1. README.md - Usage Instructions**
- How to run the mapper
- Command-line syntax
- Testing guidance
- Prerequisites

**2. customers_mapper.md - Mapping Specification**
- Complete field-by-field documentation
- Mapping rationale for each decision
- Conditional logic explanations
- Citations to Senzing specification sections
- Confidence scores for each mapping

**3. customers_mapper.py - Python Implementation**
- Production-ready mapper code
- CSV input, JSONL output
- Error handling
- Conditional logic for PERSON vs ORGANIZATION
- Dynamic identifier routing
- ~150-200 lines of well-commented Python

### Review the Generated Files

Navigate to `workshop/workspace/customers/` and open each file:

**Review customers_mapper.py:**
- Can you follow the conditional logic?
- Does it handle both PERSON and ORGANIZATION correctly?
- Is the identifier routing clear?

**Review customers_mapper.md:**
- Does it explain all mapping decisions?
- Are the citations helpful for understanding?
- Would a new team member understand this mapping?

**Review README.md:**
- Can you run the mapper from these instructions?
- Are all prerequisites listed?
- Is the testing guidance clear?

{{% notice tip %}}
**Production Ready:** These files are designed to be checked into version control. The documentation preserves the mapping knowledge for future maintenance.
{{% /notice %}}

---

## Key Takeaways

You've completed the AI-assisted mapping process:

- ✅ Loaded Senzing specifications into AI context
- ✅ Provided your source schema for analysis
- ✅ Reviewed and approved the mapping strategy
- ✅ Validated each field-by-field mapping decision
- ✅ Generated production-ready mapper code and documentation

The Mapping Assistant doesn't just generate code—it teaches you about entity resolution while guiding you through validated, best-practice mappings.

{{% notice tip %}}
**Learning Opportunity:** Please ask the AI questions as you go!  This teaches you what makes a valid Senzing JSON record and common mapping mistakes to avoid.
{{% /notice %}}

{{% notice info %}}
**Checkpoint:** You should have three files in `workshop/workspace/customers/`: `customers_mapper.py`, `customers_mapper.md`, and `README.md`. Review them to ensure they match your requirements.
{{% /notice %}}
