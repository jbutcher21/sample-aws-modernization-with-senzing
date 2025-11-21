---
title: "Step 1: Workflow Summary"
weight: 61
---

## Complete Mapping Workflow at a Glance

This table provides a roadmap of the critical steps and key decisions in the watchlist mapping workflow. **Unlike Exercise 1, this mapping is more complex—you'll need to take charge of the process**, questioning AI assumptions, verifying decisions against actual data, and driving the workflow to completion.

{{% notice tip %}}
**Your Role**: Use this guide to ensure you hit every critical step and address important decisions along the way. The prompts shown are examples from a real session—yours will differ based on your questions and the AI's responses. Focus on the decision-making patterns, not exact prompts.
{{% /notice %}}

---

## Important Notes Before You Start

### 1. You Are In Charge

This is an AI-assisted mapping workflow, not a fully automated one. You must actively manage the process to ensure quality results.

Throughout this workflow, don't be afraid to:
- **Ask for clarification** if you don't understand something - ask it what it means by ...
- **Interrupt if** the AI moves to the next step when you still have questions
- **Question decisions** - Request pros and cons if presented with options
- **Direct it** to re-examine data or revisit previous steps as needed

{{% notice tip %}}
**To interrupt the AI**: Press the stop button on the lower right of the prompt box.
{{% /notice %}}

{{% notice tip %}}
**Use copy/paste**: You can copy and paste text from the AI's response into the prompt and ask what it means.
{{% /notice %}}

---

### 2. What To Do If Things Go Wrong

**Context Loss**

AI tools have limited memory (context window). The longer your mapping session, the more likely you'll encounter issues:

**What happens when context gets full:**
- The AI may ask to compact/summarize - **say YES** or it will lose all context
- It may forget how to follow steps or execute tools correctly
- You'll notice it keeps trying different things because it's failing

**The solution is simple: Interrupt it if necessary and remind it of its context!**

**The @ command is your friend:**
- `@senzing` - Reloads the entire senzing directory (if it looses all context)
- `@senzing_mapping_assistant.md` - Reloads just the mapping workflow (it it lost context)
- `@SENZING_TOOLS_REFERENCE.md` - Reloads tool documentation (if it forgets how to run a tool)

**Ask if it knows where it's at and remind it if necessary:**
- "Do you recall where we were at?"
- "Lets revisit the mapping of persons"
- "We just took the snapshot, check the ftm directory for it and continue"

**MCP Server stops working:**

If you ask it to get an entity and it doesn't use the MCP server (tries other methods or says entity not found):
- Go back to Setup and Configuration → MCP Setup
- Open the edit screen and simply save (no changes needed)
- This reconnects the MCP server and it will start working again

**Things feel off track and you're not sure what to do:**

Sometimes it just gets too messy. **Start fresh:**
- Close the chat window
- Open a new one
- Use `@senzing` to reload context and start from generating the schema
- The workflow is designed to be simple - you'll be back on track quickly


### 3. Understand the FTM Watchlist Data

**What is this data?**

The FollowTheMoney (FTM) format contains sanctioned entities - both persons and companies - along with their relationships (ownership, directorships, etc.). This is fundamentally different from the simple customer CSV you worked with in Exercise 1.

**Know why are you mapping it**

You're loading this watchlist data to:
- See if any of your customers are sanctioned entities
- Discover relationships between entities you should be aware of
- Understand networks of connected persons and companies

### 4. Entities vs. Features - A Critical Distinction

**In Senzing, an entity is ONLY a person or a company.**

Entities have:
- Names (NAME_FIRST, NAME_LAST, NAME_ORG)
- Addresses
- Identifiers (SSN, passport, etc.)
- Other attributes

**The FTM file has multiple schemas, but only Person and Company are entities.**

Everything else (Sanctions, Ownership, Directorship, Identifiers, Addresses) are **features of entities**, not entities themselves. **See outcome [②](#outcome-stage2)**


---

## Workflow At A Glance

{{% notice tip %}}
**The AI often knows the next step and will ask if you're ready to proceed.**

- Say "yes" if you're ready to move forward
- Ask questions if you need clarification before proceeding
- Use the starting prompts below to redirect it if needed
{{% /notice %}}

| Step | Starting Action / Prompt |
|------|--------------------------|
| **0. Start fresh** | **IMPORTANT:** Open a new chat window, start with `@senzing` and press enter|
| **1. Open the data file** | Open `workspace/watchlist/ftm.jsonl` in the editor. Notice the `schema` attribute. **See outcome [①](#step1-open-ftm)** |
| **2. Generate schema** | "check the schema generator parameters and generate a schema for the ftm file grouping by the schema attribute" |
| **3. Continue mapping assistant** | "Start the senzing mapping assistant to map the ftm schema"|
| - **Stage 1: INIT** | AI loads reference files automatically |
| - **Stage 2: INVENTORY** | "ready for stage 2". Work with it to achieve this outcome: **See outcome [②](#outcome-stage2)** |
| - **Stage 3: PLANNING** | "ready for stage 3". Work with it to achieve this outcome: **See outcome [③](#outcome-stage3)** |
| - **Stage 4: MAPPING** | "ready for stage 4". Work with it to achieve this outcome: **See outcome [④](#outcome-stage4)** |
| - **Stage 5: OUTPUTS** | "ready for stage 5" |
| **4. Validate Mapper** | "Test the mapper for me", when satisfied: "run it on the full file" |
| **5. Load the data** | "@SENZING_TOOLS_REFERENCE.md Add the data sources and load it" |
| **6. Analyze snapshot** | "take a snapshot" **See outcome [⑤](#outcome-step6)** |
| **7. MCP Server Review** | "Are any entities in all 3 data sources" **See outcome [⑥](#outcome-step7)** |

{{% notice tip %}}
**Step 5 Note**: You may need to remind the AI how to add data sources using `@SENZING_TOOLS_REFERENCE.md`. If it fails or has trouble, give it context by referencing the documentation!
{{% /notice %}}

---

## Key Outcomes to Watch For

These screenshots show what correct results should look like. They may not be verbatim, but the key points are highlighted. **Your job is to direct the AI to these outcomes if it is doing something else.**

#### <a name="step1-open-ftm"></a>① Step 1: Review the FTM File

![Step 1 Review FTM file](/images/exercise2/1-ftm-data.png)

#### <a name="outcome-stage2"></a>② Stage 2: Inventory - Field Extraction

![Stage 2 Outcome](/images/exercise2/stage2-outcome.png)

#### <a name="outcome-stage3"></a>③ Stage 3: Planning - Knows how to join the schemas

![Stage 3 Outcome](/images/exercise2/stage3-outcome.png)

#### <a name="outcome-stage4"></a>④ Stage 4: Mapping - Complete examples

![Stage 4 Outcome](/images/exercise2/stage4-outcome.png)

#### <a name="outcome-step6"></a>⑤ Step 6: Snapshot Analysis

![Step 6 Outcome](/images/exercise2/step6-outcome.png)

#### <a name="outcome-step7"></a>⑥ Step 7: MCP Server Review

![Step 7 Outcome](/images/exercise2/step7-outcome.png)

---

## Key Learning Points from This Workflow

### Interactive Decision-Making
Notice the questions asked during Stage 4 mapping. These weren't errors - they were **quality checkpoints**:
- Verifying assumptions against actual data
- Discovering edge cases (company relationships)
- Clarifying Senzing conventions (NAME_ORG vs NAME_FULL)

**Important:** Asking questions improves quality BUT consumes context. Be specific with questions. If AI warns "Context ~80% full" and offers to compact, **say YES** - this compresses the conversation so you can continue. See [Step 6](../66_analyzesnapshot/) for what happens when you decline and context recovery strategies.

### Multi-Pass Processing
FTM data required special handling:
- **Pass 1:** Process master entities (Person, Company)
- **Pass 2:** Merge relationship metadata (Sanction, Ownership, Directorship)
- **Pass 3:** Merge identifiers onto Person entities

### Validation Pipeline
Multiple validation layers caught different issues:
- **Linter:** JSON syntax and structure
- **Analyzer:** Data source configuration and feature coverage
- **Loading:** Actual entity resolution matching

### Entity Resolution Results
The final numbers tell the story:
- **42% compression** - Significant duplicate detection
- **17 cross-source matches** - Hidden connections revealed
- **Multi-jurisdictional networks** - Corporate structures mapped

