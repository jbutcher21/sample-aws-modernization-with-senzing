---
title: "Explore with AI"
chapter: false
weight: 33
---

## Using AI to Understand the Workshop Files

Rather than reading lengthy documentation, let's use AI to explore the workshop folder structure. This demonstrates a key modern development skill: asking targeted questions to quickly understand unfamiliar codebases and tools.

{{% notice tip %}}
**Why ask AI?** Instead of reading lengthy documentation, you can ask targeted questions and get immediate, contextual answers. This is a key skill for modern developers!
{{% /notice %}}

---

## Opening Amazon Q Developer

First, let's open Amazon Q Developer and give it context about the workshop folder.

Click the Amazon Q icon in the left side panel of your IDE

**Ask Amazon Q:** `Use the senzing folder as context for this session`

This tells Q to reference all the files in the senzing folder when answering your questions.

**What you should see:**

![Opening Amazon Q and setting context](/images/overview/ask_qdev0.png)

---

## Question 1: What does the senzing folder contain?

**Ask Amazon Q:** `What does the senzing folder contain?`

**What you should see:**

![Question 1 - Senzing folder contents](/images/overview/ask_qdev1.png)

{{% notice info %}}
**Expected Response:** AI should explain that the senzing folder contains prompts, reference documentation, and tools for working with Senzing entity resolution.
{{% /notice %}}

---

## Question 2: What does the mapping assistant prompt do?

**Ask Amazon Q:** `What does the mapping assistant prompt do?`

**What you should see:**

![Question 2 - Mapping assistant prompt](/images/overview/ask_qdev2.png)

{{% notice info %}}
**Expected Response:** AI should explain the 5-stage workflow (INIT → INVENTORY → PLANNING → MAPPING → OUTPUTS) and how the prompt guides you through structured data mapping.
{{% /notice %}}

---

## Question 3: What are those senzing tools and when do I use them?

**Ask Amazon Q:** `What are those senzing tools and when do I use them?`

**What you should see:**

![Question 3 - Senzing tools](/images/overview/ask_qdev3.png)

{{% notice info %}}
**Expected Response:** AI should describe the schema generator (for analyzing source data), JSON linter (for validation), and JSON analyzer (for understanding mapped output), along with when to use each.
{{% /notice %}}

---

## Wrap Up

You've now practiced using AI to understand unfamiliar tools and documentation. This skill - asking AI targeted questions about code and tools - will be essential throughout the workshop.

**Key Takeaways:**
- The `workshop/` folder contains everything you need: tools, data, and solutions
- AI can help you quickly understand complex folder structures and tools
- Asking targeted questions is faster than reading documentation cover-to-cover
