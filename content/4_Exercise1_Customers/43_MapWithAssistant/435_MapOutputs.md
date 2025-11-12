---
title: "Stage 5: OUTPUTS"
weight: 435
---

## Stage 5: OUTPUTS - Generate Code and Docs

The AI generates three files:

![Generated mapper files](/images/exercise1/3-mapping16.png)

1. **`customers_mapper.py`** - Production-ready Python mapper
2. **`customers_mapper.md`** - Detailed mapping documentation
3. **`README.md`** - Usage instructions

These are perfect files for checking into a github project!

**Open the files to review:**

![Reviewing generated files](/images/exercise1/3-mapping17.png)

Navigate to `workshop/workspace/customers/` and open each file to review:
- If you are a programmer, can you follow the mapper code?
- Does the documentation explain all decisions?
- Are there any fields you want to revisit?

{{% notice tip %}}
**Iteration is Ok!** If you want to change any mappings, you can ask Q to regenerate specific sections or start a new mapping session.
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
