+++
title = "Step 1: Workflow Summary"
weight = 61
+++

## Complete Mapping Workflow at a Glance

This table provides a complete overview of the watchlist mapping workflow. **You can complete the entire exercise by following this summary**, or dive into the detailed pages for deeper exploration.

::alert[**Quick Start**: This summary shows every prompt and action needed to map FTM watchlist data to Senzing format. Use it as a standalone guide or reference as you work through the detailed pages.]{type="warning"}

---

## Important Notes Before You Start

### 1. Your Experience May Be Different

This workflow shows what happened in a real mapping session, including:
- The specific questions asked
- Corrections made when AI assumptions were wrong
- The context loss that occurred and recovery

**Your session will likely differ:**
- AI might suggest different field mappings
- You may catch different errors
- Your data structure might require different decisions
- Context loss may happen at different points (or not at all)

Use this as a guide, not a script. The principles are what matter, not matching it exactly.

---

### 2. You Are In Charge

Notice throughout this workflow:
- **I directed the AI** to things I knew about the data
- **I questioned assumptions** when I was uncertain
- **I corrected errors** when I spotted them
- **I made final decisions** on field dispositions

**Key examples:**
- "Are you sure those are all the identifier types, and how do you know?" → Found missing identifiers
- "previous name should be name_org, not name_full" → Corrected convention error
- "You say 3 master entity types but list 2..." → Caught arithmetic mistake

**The AI is your assistant, not your replacement.** You have the domain knowledge. The AI has Senzing knowledge. Together you make good decisions.

---

::alert[### 3. What To Do If Things Go Wrong

**Context Loss (80% Warning)**
- **If AI warns "Context ~80% full" and offers to compact**: Say YES immediately
- **If you decline**: You will likely hit 100% and lose all context
- **If context is lost**: Use the recovery strategies in [Step 6](../66_analyzesnapshot/)
  - Re-explore the repository
  - Find artifacts (snapshot files, generated code)
  - Reference documentation
  - Continue from checkpoints

**AI Makes Wrong Assumptions**
- **Question it**: "How do you know?" "Are you sure?"
- **Check actual data**: Don't accept answers based on schema alone
- **Correct errors immediately**: The earlier you catch mistakes, the easier to fix

**Validation Errors**
- **Linter fails**: Fix JSON syntax errors in generated output
- **Analyzer shows critical errors**: Usually data source configuration - follow the fix steps
- **Load fails**: Check error messages for specific record issues

**Can't Continue (Session Ending/Context Full)**

**Ideally:** Use `/resume` when you return (if available in your AI tool)

**If no /resume available:** Just give context manually and tell it what to do next:

Example recovery (what actually happened):
```
You: "Its already loaded. can you find the snapshot on
     the watchlist directory and show it to me"

AI: [finds snapshot file and shows it]

You: "in the senzing tools reference it tells you how to
     summarize the snapshot, can you do that"

AI: [proceeds with analysis]
```

Simple approach:
- Tell AI where you are: "Data is loaded, snapshot is taken"
- Tell AI what to find: "Find the snapshot file in workspace/watchlist"
- Tell AI what to do next: "Analyze it according to the tools reference"

::alert[See [Step 6](../66_analyzesnapshot/) for the complete recovery example.]{type="warning"}

---

| Step | Action / Prompt Used | Reason / Outcome |
|------|---------------------|------------------|
| **1. Generate Schema** | **Prompt:** "Generate a schema for the ftm.jsonl file I have open"
**AI runs:** `python3 senzing/tools/sz_schema_generator.py workspace/watchlist/ftm.jsonl -o workspace/watchlist/ftm_schema.md` | Understand the FTM data structure: 73 records, 5 schema types (Person, Company, Sanction, Ownership, Directorship), 31 unique fields |
| **2. Start AI Mapping** | **Prompt:** "@senzing"
**Then:** "Yes" [to start AI-assisted mapping] | Load AI mapping assistant to guide through 5-stage workflow |
| **Stage 1: INIT** | AI loads 5 reference files: entity spec, examples, linter, identifier crosswalk, usage type crosswalk | Provides AI with complete Senzing knowledge base and validation tools |
| **Stage 2: INVENTORY** | **Prompt:** "yes" [to proceed]
AI extracts all 31 fields from schema | Creates complete field inventory: root fields, Person attributes, relationship fields, identifier fields, sanction metadata. Integrity check: 31 extracted = 31 displayed |
| **Stage 3: PLANNING** | AI identifies master entities (Person, Company) and DATA_SOURCE codes (SANCTIONS, CORP_FILINGS) | **Your correction:** "You say 3 master entity types but list 2: person and company. What is the third?"
**Result:** Corrected to 2 master types, 3 relationship types |
| **Stage 4: MAPPING** | **Prompt:** "Show me the full mapping table first"
AI maps each field to Senzing features, payload, or ignored | **Key decisions:** Sanction records merge as payload, Ownership/Directorship become REL_POINTER relationships, identifiers merge onto Person entities |
| **Question: Identifier Types** | **Prompt:** "Are you sure those are all the identifier types, and how do you know?" | **Correction:** AI checked actual data and found DRIVERS_LICENSE and SSN (not just assumed from schema) |
| **Question: Company Relationships** | **Prompt:** "I didn't see any rel_pointers in the json examples, don't companies have relationships as well?" | **Discovery:** Found company-to-company ownership (Universal Exports owns 3 subsidiaries) |
| **Question: Relationship Roles** | **Prompt:** "What are my options for assigning roles to relationship pointers"
**Your decision:** "The principal and president" | **Result:** Use OWNER_OF for ownership, PRINCIPAL_OF/PRESIDENT_OF for directorships based on role values |
| **Question: Previous Names** | **Your correction:** "previous name should be name_org, not name_full" | **Fix:** For organizations, use NAME_ORG for previous names |
| **Question: Company Identifiers** | **Prompt:** "Aren't there any identifiers for companies?" | **Result:** None in this dataset |
| **Stage 5: OUTPUTS** | **Prompt:** "yes" [to proceed to JSON generation]
**Then:** "ok show me company json record examples and lint" | Complete mapping implementation with multi-pass processing for relationships. AI generates README.md, ftm_mapper.md (spec), ftm_mapper.py (code) |
| **3. Run Mapper** | **Prompt:** "ok lets run it on the actual data"
**AI runs:** `python3 ftm_mapper.py ftm.jsonl ftm_senzing.jsonl` | **Result:** 39 Senzing entities generated from 73 FTM records |
| **4. Lint Output** | AI automatically runs: `python3 senzing/tools/lint_senzing_json.py ftm_senzing.jsonl` | **Result:** ✅ PASSED - No JSON syntax errors |
| **5. Analyze Quality** | **Prompt:** "I didn't see any errors or warnings. please run the json analyzer again according to tools reference documentation"
**AI runs:** `python3 senzing/tools/sz_json_analyzer.py ftm_senzing.jsonl -o analysis.md` | **Result:** ❌ Critical errors - DATA_SOURCE not found: CORP_FILINGS, SANCTIONS |
| **6. Configure Data Sources** | **Prompt:** "I updated the senzing config. Run the json analyzer again"
**Then:** "yes" [to configure data sources]
**AI creates config and runs:** `sz_configtool -f ftm_config.g2c` | **Result:** ✅ Both data sources registered |
| **7. Re-analyze** | AI runs: `python3 senzing/tools/sz_json_analyzer.py ftm_senzing.jsonl -o analysis.md` | **Result:** ✅ Critical Errors: 0 (resolved!), 13 Senzing features with good coverage |
| **8. Load Data** | **Prompt:** "ok load it"
**AI runs:** `sz_file_loader -f ftm_senzing.jsonl` | **Result:** ✅ 39 records loaded, 0 errors, 0.0 minutes, 259 candidate matches evaluated |
| **9. Take Snapshot** | **Prompt:** "ok take a snapshot"
**AI runs:** `sz_snapshot -o ftm-watchlist-snapshot-$(date +%Y-%m-%d) -Q` | Captures entity resolution statistics for analysis |
| **--- CONTEXT LOST ---** | **Session ended** → Context hit 100%, session reset | See Step 6 for what happened and recovery |
| **10. Recover Context** | **New session - Prompt:** "did you compact"
**AI:** ❌ No memory of previous work | Had to recover by finding snapshot file |
| **11. Find Snapshot** | **Prompt:** "@senzing" [re-explore]
**Then:** "do you still have access to the senzing mcp server?"
**Then:** "Its already loaded. can you find the snapshot on the watchlist directory and show it to me" | AI locates: ftm-watchlist-snapshot-2025-11-14.json |
| **12. Analyze Snapshot** | **Prompt:** "in the senzing tools reference it tells you how to summarize the snapshot, can you do that" | **Result:** 92 entities from 159 total records (42% compression), 17 cross-source matches |
| **13. Find Multi-Source Entity** | **Prompt:** "show that multi source entity"
**AI uses:** `get_entity(91)` via MCP server | **Discovery:** Alexander Vasiliev spans CUSTOMERS, SANCTIONS, CORP_FILINGS with Cyrillic name variants |
| **14. Resolution Timeline** | **Prompt:** "how did this entity come together"
**AI uses:** `how_entity_resolved(91)` | **Insight:** Cross-language name matching (Cyrillic→Latin) and international phone format variations |
| **15. Map Relationships** | **Prompt:** "show his relationships in a simple graph view"
**AI uses:** `get_entity()` calls for related entities | **Network:** Alexander Vasiliev owns Mullenkrants Autoworks, Faisal Siddiqui is President |

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

---

::alert[**Next Steps**: Continue to the detailed pages to see the full prompts, responses, and teaching moments, or jump straight to mapping your own FTM data using this workflow as a guide.]{type="warning"}
