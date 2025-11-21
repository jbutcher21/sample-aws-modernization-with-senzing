---
title: "Workflow Steps"
weight: 62
---

## Complete Mapping Workflow

Follow these steps to map the FTM watchlist data to Senzing format. Each step includes example prompts and references to key outcomes you should achieve.

{{% notice tip %}}
**The AI often knows the next step and will ask if you're ready to proceed.**

- Say "yes" if you're ready to move forward
- Ask questions if you need clarification before proceeding
- Use the starting prompts below to redirect it if needed
{{% /notice %}}

---

## Workflow Steps

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

---

## Key Outcomes to Watch For

These screenshots show what correct results should look like at critical stages in the workflow. They may not be verbatim, but the key points are highlighted.

**Your job is to direct the AI to these outcomes if it is doing something else.**

{{% notice tip %}}
**Having trouble?** You can copy/paste the screenshot into the prompt and tell the AI "this is the result I'm looking for!"
{{% /notice %}}

---

### <a name="step1-open-ftm"></a>① Step 1: Review the FTM File

When you open the `ftm.jsonl` file, you should notice:
- JSON format with one record per line
- A `schema` attribute indicating record type (Person, Company, Sanction, etc.)
- Nested structures with properties arrays
- International character sets (Cyrillic, Arabic, Latin)

![Step 1 Review FTM file](/images/exercise2/1-ftm-data.png)

---

### <a name="outcome-stage2"></a>② Stage 2: Inventory - Field Extraction

At Stage 2, the AI should extract all 31 unique fields from the schema and categorize them:
- Root fields (id, schema, properties, referents)
- Person/Company attributes (name, alias, birthDate, nationality, etc.)
- Relationship fields (ownership, directorship)
- Sanction metadata (program, authority, startDate)

**Critical understanding:** Only Person and Company schemas are entities. Everything else (Sanctions, Ownership, Directorship) are **features that merge onto entities**.

![Stage 2 Outcome](/images/exercise2/stage2-outcome.png)

---

### <a name="outcome-stage3"></a>③ Stage 3: Planning - Knows How to Join Schemas

At Stage 3, the AI should identify:
- **2 master entity types:** Person and Company
- **3 relationship types:** Sanction (metadata), Ownership (REL_POINTER), Directorship (REL_POINTER)
- **DATA_SOURCE codes:** SANCTIONS for watchlist records, CORP_FILINGS for corporate relationships
- **Processing strategy:** Multi-pass (masters first, then metadata, then relationships)

The AI should understand how Sanction records reference Person/Company IDs and need to merge as payload.

![Stage 3 Outcome](/images/exercise2/stage3-outcome.png)

---

### <a name="outcome-stage4"></a>④ Stage 4: Mapping - Complete Examples

At Stage 4, the AI should show complete mapping examples for:
- **Person entities** with names, addresses, identifiers
- **Company entities** with NAME_ORG and addresses
- **Sanction payloads** merging onto Person/Company
- **Ownership relationships** using REL_POINTER with OWNER_OF role
- **Directorship relationships** using REL_POINTER with PRINCIPAL_OF/PRESIDENT_OF roles

Each example should include proper RECORD_ID, DATA_SOURCE, and RECORD_TYPE.

![Stage 4 Outcome](/images/exercise2/stage4-outcome.png)

---

### <a name="outcome-step6"></a>⑤ Step 6: Snapshot Analysis

After loading data and taking a snapshot, you should see:
- **92 entities** created from 159 total records (42% compression)
- **17 cross-source matches** showing connections between CUSTOMERS, SANCTIONS, and CORP_FILINGS
- Breakdown showing single-source vs multi-source entities
- Entity distribution across the three data sources

This demonstrates successful entity resolution across all three datasets.

![Step 6 Outcome](/images/exercise2/step6-outcome.png)

---

### <a name="outcome-step7"></a>⑥ Step 7: MCP Server Review

Using the MCP server to investigate entities appearing in all 3 data sources, you should discover:
- **Alexander Vasiliev** (Entity 91) appears in CUSTOMERS, SANCTIONS, and CORP_FILINGS
- Multiple name variants including Cyrillic and Latin transliterations
- Ownership relationship to Mullenkrants Autoworks
- Connection to Faisal Siddiqui through company directorship
- Cross-language name matching and international phone format resolution

This demonstrates the power of entity resolution to reveal hidden networks.

![Step 7 Outcome](/images/exercise2/step7-outcome.png)

