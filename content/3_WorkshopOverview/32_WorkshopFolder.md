---
title: "Workshop Folder Tour"
chapter: false
weight: 32
---

## Opening Your Workshop Environment

All workshop materials are located in the `/home/ubuntu/workshop/` directory.

**Open this folder now in your IDE:**
1. In your code-server IDE, use the file explorer (left sidebar)
2. Navigate to `/home/ubuntu/workshop/`
3. Expand the folders to see the structure

## The Workshop Folder Structure

![Opening the workshop folder in your IDE](/images/overview/workshop_open.png)

```
workshop/
├── senzing/           # Senzing toolkit - prompts, references, tools
├── workspace/         # Your source data for exercises
└── solutions/         # Complete reference implementations
```

{{% notice tip %}}
Solutions are provided so you can catch up if you fall behind or check your work. Try the exercise yourself first - that's where the learning happens!
{{% /notice %}}

---

## The `senzing/` Folder

**What it contains:** Everything you need to work with Senzing and AI

```
senzing/
├── prompts/
│   └── senzing_mapping_assistant.md      # 5-stage AI workflow prompt
├── reference/
│   ├── senzing_entity_specification.md   # Complete Senzing feature documentation
│   ├── senzing_mapping_examples.md       # Real-world mapping examples
│   ├── identifier_crosswalk.json         # Identifier type lookup table
│   └── usage_type_crosswalk.json         # Valid usage types for features
├── tools/
│   ├── sz_schema_generator.py            # Analyzes source data structure
│   ├── lint_senzing_json.py              # JSON validator for Senzing format
│   ├── sz_json_analyzer.py               # Analyzes mapped Senzing output
│   └── sz_default_config.json            # Reference Senzing configuration
└── SENZING_TOOLS_REFERENCE.md            # Complete tool documentation
```

Rather than documenting each tool in detail here, let's explore them using AI assistance!

**Try this now:**
1. Open Amazon Q Developer in your IDE
2. Reference the senzing folder using `@senzing` to give Q context
3. Ask questions about specific tools or files

Remember: All AI assistants work better with context!

<video width="800" controls>
  <source src="/images/overview/open_qdev_senzing.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

---

## Explore with AI: Question the Workshop Structure

Now that you've seen the folder structure, let's use AI to understand what's in these folders. This demonstrates how AI can help you learn unfamiliar codebases and tools.

{{% notice tip %}}
**Why ask AI?** Instead of reading lengthy documentation, you can ask targeted questions and get immediate, contextual answers. This is a key skill for modern developers!
{{% /notice %}}

### Question 1: What does the senzing folder contain?

**Ask Amazon Q:**
```
What does the senzing folder contain?
```

**What you should see:**

![Question 1 - Senzing folder contents](/images/overview/q1_senzing_folder_placeholder.png)

{{% notice info %}}
**Expected Response:** AI should explain that the senzing folder contains prompts, reference documentation, and tools for working with Senzing entity resolution.
{{% /notice %}}

---

### Question 2: What does the mapping assistant prompt do?

**Ask Amazon Q:**
```
What does the mapping assistant prompt do?
```

**What you should see:**

![Question 2 - Mapping assistant prompt](/images/overview/q2_mapping_prompt_placeholder.png)

{{% notice info %}}
**Expected Response:** AI should explain the 5-stage workflow (INIT → INVENTORY → PLANNING → MAPPING → OUTPUTS) and how the prompt guides you through structured data mapping.
{{% /notice %}}

---

### Question 3: What are those senzing tools and when do I use them?

**Ask Amazon Q:**
```
What are those senzing tools and when do I use them?
```

**What you should see:**

![Question 3 - Senzing tools](/images/overview/q3_senzing_tools_placeholder.png)

{{% notice info %}}
**Expected Response:** AI should describe the schema generator (for analyzing source data), JSON linter (for validation), and JSON analyzer (for understanding mapped output), along with when to use each.
{{% /notice %}}

---

## Wrap Up

You've now explored the workshop folder structure and practiced using AI to understand unfamiliar tools and documentation. This skill - asking AI targeted questions about code and tools - will be essential throughout the workshop.

{{% notice tip %}}
**Next Step:** Now that you understand the workshop structure, you're ready to learn about Senzing's AI-assisted mapping solution!
{{% /notice %}}

**Key Takeaways:**
- The `workshop/` folder contains everything you need: tools, data, and solutions
- AI can help you quickly understand complex folder structures and tools
- Asking targeted questions is faster than reading documentation cover-to-cover