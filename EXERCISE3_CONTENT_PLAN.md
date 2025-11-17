# Exercise 3: Customer Mapping - Content Distribution Plan

Based on the conversation in `customer-conversation.md`, here's how content should be distributed across the exercise pages:

## Step 1: Examine Source Data (41_ExamineSourceData.md)
**Content from conversation:** Lines 10-23 (Initial setup and senzing folder exploration)
- What the senzing folder contains
- Overview of prompts, reference files, and tools
**Screenshot recommendations:**
- Screenshot of folder structure
- Screenshot showing tool reference documentation

## Step 2: Generate Schema (42_CreateSchema.md) ✅ Already good
**Content from conversation:** Lines 53-63 (Schema generation)
- Schema generator output showing 120 records, 19 fields
- Field statistics and population rates
**Screenshot recommendations:**
- Schema generation command and approval dialog
- Complete schema output with all 19 fields

## Step 3: Map with Assistant - Parent Page (43_MapWithAssistant/_index.md)
**Content from conversation:** Lines 28-36 (Mapping assistant overview)
- Overview of 5-stage workflow
- Key features: interactive guidance, validation, guardrails

### Stage 1: INIT (431_MapInit.md)
**Content from conversation:** Lines 70-79 (STAGE 1: INIT)
- Loading all 5 reference files
- Validating linter tool availability
**Screenshot recommendations:**
- Loading references confirmation

### Stage 2: INVENTORY (432_MapInventory.md)
**Content from conversation:** Lines 81-88 (STAGE 2: INVENTORY)
- Enumeration of all 19 source fields
- Field categorization
**Screenshot recommendations:**
- Field extraction and categorization output

### Stage 3: PLANNING (433_MapPlanning.md)
**Content from conversation:** Lines 91-98 (STAGE 3: PLANNING)
- DATA_SOURCE naming (CUSTOMERS)
- Entity logic (customer_type controls RECORD_TYPE)
- Single pass with conditional mapping strategy
**Screenshot recommendations:**
- Planning strategy presentation

### Stage 4: MAPPING (434_MapMapping.md)
**Content from conversation:** Lines 101-116 (STAGE 4: MAPPING)
- Complete field disposition table with confidence scores
- 7 features mapped, 4 payload fields
- Dynamic identifier handling (id_type/id_number/id_country)
- Sample JSON validation with linter
**Screenshot recommendations:**
- Field mapping table with confidence scores
- Sample JSON records
- Linter validation success

### Stage 5: OUTPUTS (435_MapOutputs.md)
**Content from conversation:** Lines 120-128 (STAGE 5: OUTPUTS)
- Three generated files: README.md, customers_mapper.md, customers_mapper.py
- Final statistics: 1 entity type, 19 fields, 7 features, 4 payload types
**Screenshot recommendations:**
- Generated files list
- Code preview of mapper

## Step 4: Validate Mapping (44_ValidateMapping.md)
**Content from conversation:** Lines 133-142 (Mapper execution)
- Running mapper on full dataset
- 120 records processed successfully
- Address handling fix
**Screenshot recommendations:**
- Mapper execution command and output
- 120 records written confirmation

## Step 5: Load Data (45_LoadData.md)
**Content from conversation:** Lines 144-165 (Data loading and configuration)
- Adding CUSTOMERS data source with sz_configtool
- Loading with sz_file_loader
- 120 records loaded, 8 redo records
**Screenshot recommendations:**
- Config tool adding data source
- File loader progress and completion
- Load statistics

## Step 6: Take Snapshot (46_TakeSnapshot.md)
**Content from conversation:** Lines 162-165 (Snapshot generation)
- sz_snapshot command execution
- 78 entities created from 120 records
**Screenshot recommendations:**
- Snapshot command
- Snapshot completion message

## Step 7: Analyze Snapshot (47_AnalyzeSnapshot.md)
**Content from conversation:** Lines 171-207 (Analysis results)
- Compression statistics: 120→78 entities (35% compression)
- Match breakdown: 39 definitive, 14 possible matches, 13 possible relations
- Top 5 match keys at each level with detailed explanations
**Screenshot recommendations:**
- Snapshot statistics summary
- Match key breakdown table
- Top matching patterns visualization

## Step 8: Review with MCP (48_ReviewWithMCP.md)
**Content from conversation:** Lines 210-331 (Entity investigation)

### Section 1: Entity Profile Example
- Entity 1 profile (Robert Smith - 4 merged records)
- Source records table showing merge evidence
- Resolved features

**Screenshot recommendations:**
- Entity 1 profile display
- Record merge timeline

### Section 2: Resolution Logic
- How Entity 1 was resolved (3 progressive merge steps)
- Match keys and rules used
- Feature matching scores

**Screenshot recommendations:**
- Step-by-step resolution explanation
- Match score visualization

### Section 3: Relationship Analysis
- Entity 1 to Entity 2 relationship (POSSIBLY_SAME)
- Why Entity 2 didn't merge (missing supporting features)
- Side-by-side comparison table

**Screenshot recommendations:**
- Relationship graph
- Side-by-side feature comparison

### Section 4: NAME+DOB+ADDRESS Match Example
- Entity 3 (Eddie/Edward Kusha match)
- Triple confirmation match analysis
- Family relationships detected

**Screenshot recommendations:**
- NAME+DOB+ADDRESS match visualization
- Family relationship network

## Key Content Themes Throughout:

1. **Interactive Learning:** Emphasize asking questions and exploring
2. **Validation at Each Step:** Show checkpoints and validation
3. **Real Results:** Use actual numbers and examples from the session
4. **Business Value:** Explain why 35% compression matters
5. **Match Quality:** Show how Senzing prevented false positives

## Screenshot Naming Convention:
`/static/images/exercise3/`
- `1-examine-[topic].png`
- `2-schema-[topic].png`
- `3-mapping[stage]-[topic].png`
- `4-validate-[topic].png`
- `5-load-[topic].png`
- `6-snapshot-[topic].png`
- `7-analyze-[topic].png`
- `8-mcp-[topic].png`
