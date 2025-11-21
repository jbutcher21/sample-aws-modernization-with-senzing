+++
title = "Workshop Folder Tour"
chapter = false
weight = 32
+++

## Opening Your Workshop Environment

All workshop materials are located in the `/home/ubuntu/workshop/` directory.

In this section, you'll explore the workshop folder structure and learn how AI can help you quickly understand unfamiliar tools and documentation - a key skill you'll use throughout the workshop.

**Open this folder now in your IDE:**
1. In your code-server IDE, use the file explorer (left sidebar)
2. Navigate to `/home/ubuntu/workshop/`
3. Expand the folders to see the structure

## The Workshop Folder Structure

![Workshop folder in your IDE](/images/overview/workshop_open.png)

### Here is a brief explanation of the main folders and their contents:

```
workshop/
├── senzing/                              # Senzing toolkit - prompts, references, tools
│   ├── prompts/
│   │   └── senzing_mapping_assistant.md      # 5-stage AI workflow prompt
│   ├── reference/
│   │   ├── senzing_entity_specification.md   # Complete Senzing feature documentation
│   │   ├── senzing_mapping_examples.md       # Real-world mapping examples
│   │   ├── identifier_crosswalk.json         # Identifier type lookup table
│   │   └── usage_type_crosswalk.json         # Valid usage types for features
│   ├── tools/
│   │   ├── sz_schema_generator.py            # Analyzes source data structure
│   │   ├── lint_senzing_json.py              # JSON validator for Senzing format
│   │   ├── sz_json_analyzer.py               # Analyzes mapped Senzing output
│   │   └── sz_default_config.json            # Reference Senzing configuration
│   └── SENZING_TOOLS_REFERENCE.md            # Complete tool documentation
├── workspace/                            # Your source data for exercises
└── solutions/                            # Complete reference implementations
```

::alert[The solutions folder is provided so you can catch up if you fall behind or check your work. Try the exercise yourself first - that's where the learning happens!]{type="info"}

---

Ready to explore the workshop materials with AI assistance? Let's move to the next page where you'll practice asking AI questions about the folder structure!