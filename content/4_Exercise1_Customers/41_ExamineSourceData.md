---
title: "Step 1: Explore Senzing"
weight: 41
---

## Understanding Senzing Workshop Resources

Before diving into mapping, it's valuable to understand what resources Senzing provides to help you succeed. In this step, you'll explore the `senzing/` folder structure and learn about the tools and references available.

## Open the Workshop Folder

First, open the workshop folder in your IDE to see the project structure.

**In your IDE file explorer:**
1. Navigate to the `workshop/` directory
2. Expand the folder to see its contents

![Basic Navigation and open folder](/images/exercise1/0-open.png)

## Add the Senzing folder as context

**Add context to Amazon Q:**

1. Open Amazon Q Developer (if not already open)
2. In the Q chat input field, type `@` to open the context menu
3. Select the `senzing` folder from the list
4. Press Enter to add it as context

![Adding senzing folder as context](/images/exercise1/0-context.png)

{{% notice note %}}
**Important:** When AI's fail it is because they do not have enough context. So let's add the senzing folder as context for this exercise. Later on, if you find the AI not responding properly, try using the @ sign again to remind it!
{{% /notice %}}

Now ask Amazon Q to explain what the senzing folder contains.

**Tell Amazon Q:** `@senzing What does the senzing folder contain?`

![Senzing folder structure](/images/exercise1/1-folders.png)

### What You'll Discover

The `senzing/` folder contains workshop materials organized into 4 key sections:

**1. Prompts (`prompts/`)**
- **Senzing Mapping Assistant** - The AI prompt that guides you through the 5-stage mapping workflow
- This is what orchestrates the entire mapping process you'll use in Step 3

**2. Reference Materials (`reference/`)**
- **senzing_entity_specification.md** - The complete Senzing entity model (2,100+ lines)
- **Mapping examples** - Real-world mapping patterns
- **Crosswalk tables** - Identifier and usage type mappings
- **Entity diagrams** - Visual guides to the data model

**3. Tools (`tools/`)**
- **sz_schema_generator.py** - Analyzes CSV files and generates schema documents
- **lint_senzing_json.py** - Validates JSON format during development
- **sz_json_analyzer.py** - Checks data quality before loading
- **Config and loader utilities** - For Senzing environment setup

**4. Documentation**
- **SENZING_TOOLS_REFERENCE.md** - Complete tool usage guide

## Understanding the Mapping Assistant

The Mapping Assistant is the key to this exercise. Ask Q to explain what it does.

**Ask Amazon Q:** `What does the mapping assistant prompt do?`

![Mapping Assistant Prompt](/images/exercise1/2-prompt.png)

### The 5-Stage Mapping Workflow

The assistant creates a structured process:

1. **INIT** - Loads references and validates tools
2. **INVENTORY** - Extracts all source fields
3. **PLANNING** - Identifies entities and DATA_SOURCE codes
4. **MAPPING** - Dispositions fields as Feature/Payload/Ignore
5. **OUTPUTS** - Generates README, specification, and mapper code

**Key features:**
- Interactive guidance at each stage
- Built-in validation with linter
- Guardrails against AI hallucination
- Citations for all mapping decisions

## Learn About the Tools

**Ask Amazon Q:** `What are those senzing tools and when do I use them?`

![Tools reference explanation](/images/exercise1/3-tools.png)

### Tool Workflow

**Standard workflow order:**
1. **Schema Generator** → Analyze source data structure
2. **AI Mapping** → Use Mapping Assistant to create mapper
3. **Analyzer** → Check quality of mapped output
4. **Config Tool** → Configure data sources in Senzing
5. **Loader** → Load data into Senzing
6. **Snapshot** → Analyze resolution results

{{% notice tip %}}
**Workshop Development Tools** (Python scripts) work anywhere. **Senzing Core Tools** require the Senzing environment to be configured.  (Already done in this workshop)
{{% /notice %}}

{{% notice info %}}
**Checkpoint:** You should understand the senzing folder structure, the 5-stage Mapping Assistant workflow, and when to use each tool.
{{% /notice %}}
