---
title: "Before You Start"
weight: 61
---

## Overview

This exercise is more complex than Exercise 1. **You'll need to take charge of the process**, questioning AI assumptions, verifying decisions against actual data, and driving the workflow to completion.

{{% notice tip %}}
**Your Role**: The prompts shown throughout this exercise are examples from a real session—yours will differ based on your questions and the AI's responses. Focus on the decision-making patterns, not exact prompts.
{{% /notice %}}

---

## 1. You Are In Charge

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

## 2. What To Do If Things Go Wrong

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


---

## 3. Understand the FTM Watchlist Data

**What is this data?**

The FollowTheMoney (FTM) format contains sanctioned entities - both persons and companies - along with their relationships (ownership, directorships, etc.). This is fundamentally different from the simple customer CSV you worked with in Exercise 1.

**Know why are you mapping it**

You're loading this watchlist data to:
- See if any of your customers are sanctioned entities
- Discover relationships between entities you should be aware of
- Understand networks of connected persons and companies

---

## 4. Entities vs. Features - A Critical Distinction

**In Senzing, an entity is ONLY a person or a company.**

Entities have:
- Names (NAME_FIRST, NAME_LAST, NAME_ORG)
- Addresses
- Identifiers (SSN, passport, etc.)
- Other attributes

**The FTM file has multiple schemas, but only Person and Company are entities.**

Everything else (Sanctions, Ownership, Directorship, Identifiers, Addresses) are **features of entities**, not entities themselves. You'll see this distinction clearly in Stage 2 of the mapping workflow.

---

{{% notice info %}}
**Ready?** Continue to the next page to see the complete workflow steps and key outcomes to watch for.
{{% /notice %}}
