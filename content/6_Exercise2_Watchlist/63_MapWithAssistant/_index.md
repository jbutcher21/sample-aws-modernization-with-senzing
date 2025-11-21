+++
title = "Step 3: Map with Senzing AI Assistant"
weight = 63
+++

## The 5-Stage Mapping Workflow

Now that you understand the FTM data structure, it's time to map it to Senzing format using the **Senzing Mapping Assistant** - an AI-guided workflow with 5 structured stages.

{{% notice warning %}}**AI-Assisted Mapping**: The Senzing Mapping Assistant is a prompt-based system that guides an AI through the complete mapping process. It has access to all Senzing documentation, examples, and validation tools, making it an expert mapping partner.]{type="info"}

---

## The Five Stages

Each stage has a specific purpose and validation checkpoints:

| Stage | Name | Purpose | Output |
|-------|------|---------|--------|
| **1** | [INIT](631_mapinit/) | Load reference files and test tools | AI has complete Senzing knowledge base |
| **2** | [INVENTORY](632_mapinventory/) | Extract all fields from schema | Complete field list with integrity check |
| **3** | [PLANNING](633_mapplanning/) | Determine DATA_SOURCE and entity types | Processing strategy for complex data |
| **4** | [MAPPING](634_mapmapping/) | Map each field to Senzing format | Field disposition: Feature, Payload, or Ignored |
| **5** | [OUTPUTS](635_mapoutputs/) | Generate code and documentation | Mapper script, spec, and sample output |

---

## How This Differs from Exercise 1

**Exercise 1 (Customer CSV):**
- Walked through every prompt and response with screenshots
- Detailed explanation of each decision
- Every field discussed individually

**Exercise 2 (FTM Watchlist):**
- Shows key prompts and results
- Highlights decision points and corrections
- Demonstrates how to handle complex data
- **You can complete this faster by learning from Exercise 1 patterns**

{{% notice info %}}**Efficiency Note**: If you completed Exercise 1, you already understand the workflow. Use this exercise to see how the same process handles more complex data structures and relationships.{{% /notice %}}

---

## Starting the Mapping Process

To begin AI-assisted mapping, you need to load the Senzing Mapping Assistant prompt. There are two ways to do this:

**Option 1: Using the @ reference (if available)**
```
@senzing
```

**Option 2: Explicitly load the prompt file**
```
Read and follow the instructions in:
/home/ubuntu/workshop/senzing/prompts/senzing_mapping_assistant.md
```

Once loaded, the AI will guide you through each stage, asking questions and validating decisions along the way.

---

## What to Expect

### Interactive Decision-Making
The AI will ask questions when it:
- Needs clarification on field meanings
- Encounters low-confidence mapping decisions
- Finds conflicting or unusual data patterns
- Discovers edge cases not covered in examples

### Quality Checkpoints
You'll be prompted to verify:
- All fields were extracted (no hallucinations)
- DATA_SOURCE codes are appropriate
- Field dispositions make business sense
- Sample JSON passes validation

### Iterative Corrections
Don't expect perfection on the first try! This exercise shows **real corrections made during mapping**:
- Verifying identifier types against actual data
- Discovering missed relationship patterns
- Clarifying Senzing conventions (NAME_ORG vs NAME_FULL)

{{% notice info %}}**Important**: The AI is knowledgeable but not infallible. **Your domain expertise is crucial.** Question assumptions, verify against actual data, and correct mistakes when you spot them.{{% /notice %}}

---

## Following Along

The next five pages show:
1. **Prompts used** - What was asked
2. **AI responses** - What the AI provided
3. **Your corrections** - What was adjusted and why
4. **Final decisions** - What was ultimately implemented

Each page is standalone, so you can jump to specific stages to see how particular challenges were handled.

---

::alert[**Pro Tip**: Keep three tabs open:
1. Your AI assistant (Claude, ChatGPT, etc.)
2. The schema file (`ftm_schema.md`)
3. The source data file (`ftm.jsonl`)

This lets you quickly verify AI suggestions against actual data.{{% /notice %}}

**Ready? Let's start with Stage 1: INIT →**
