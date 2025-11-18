---
title: "Step 6: Analyze Snapshot"
weight: 66
---

## Analyzing Entity Resolution Results

With data loaded and a snapshot captured, it's time to analyze the entity resolution results to understand what Senzing found.

{{% notice warning %}}
**IMPORTANT LESSON: Context Loss Across Sessions**

This step documents a real scenario that happened during workshop development. The mapping and loading were completed in one AI session, then **the session ended**. When analysis resumed in a new session, **the AI had lost all context** about what had been done.

This section shows what happened, why it happened, and how to recover - a critical skill for working with AI on multi-day projects!
{{% /notice %}}

---

## What Happened: The Context Gap

### Original Prompt (New Session)
```
did you compact
```

### AI Response
```
I'll explore the senzing directory to show you what's available for the workshop.
```

**Problem:** The AI didn't know:
- What data had been mapped
- What files existed
- What work had been completed
- What "compact" meant in this context

---

## Why Context Was Lost

In this case, context was lost because the **context window filled up** during the mapping conversation:

1. **Long Interactive Mapping Session**
   - 5-stage mapping workflow with multiple questions and corrections
   - Each question and answer consumed context tokens
   - Asking questions improves quality but uses more context

2. **Data Loading Completed**
   - All 39 records successfully loaded into Senzing ✅
   - Loading was done, data was in Senzing
   - Next step should have been: take snapshot (Senzing analysis)

3. **Context Warning Appeared**
   - AI warned: "Context ~80% full"
   - AI likely offered to **compact** (compress conversation to save tokens)
   - This was the signal: **say YES to compact**

4. **Took a Chance**
   - Said no / declined the compact offer
   - Continued without compacting the conversation
   - Kept going, probably asked to take snapshot
   - Each additional message used more tokens
   - Context filled to 100% → Session automatically reset

5. **All Context Lost**
   - When you asked "did you compact" - AI had no memory
   - The conversation was never compacted (compressed)
   - Session had reset, all context gone
   - Had to recover from scratch

### Understanding "Compact" vs "Take Snapshot"

**THESE ARE COMPLETELY DIFFERENT:**

**COMPACT** (AI Feature):
- AI action to compress/summarize conversation context
- Reduces token count by condensing the conversation
- Allows you to continue in the same session
- Prevents hitting the 100% limit
- Example: AI says "Would you like me to compact the conversation?" → Say YES!

**TAKE SNAPSHOT** (Senzing Tool):
- Senzing command: `sz_snapshot`
- Analyzes loaded entities and generates statistics
- Creates JSON file with entity counts, compression rates, cross-source matches
- Has nothing to do with AI context management
- This is a data analysis step, not a context management step

Compacting the conversation:
- ✅ **Prevents context loss** by compressing conversation history
- ✅ **Lets you continue** in the same session
- ✅ **Reduces token count** so you have room to keep working
- ✅ **Preserves enough context** to maintain continuity

{{% notice warning %}}
**The Lesson: Accept the Compact Offer**

When AI warns "Context ~80% full" and offers to compact:
- **SAY YES** to the compact offer
- AI will compress the conversation history
- This frees up tokens to continue working
- You can then take snapshot, analyze results, etc. in the same session

**DON'T** decline and hope for the best - at 100%, session WILL reset automatically.

**In this exercise:** Data was loaded, ready to take snapshot. Context hit 80%, AI offered to compact. Should have said "yes, compact the conversation." Instead, took a chance and declined. Kept going without compacting → hit 100% → session reset → all context lost.
{{% /notice %}}

---

## How to Recover: Step-by-Step

### Recovery Step 1: Re-establish Context

**Your Prompt:**
```
@senzing
```

**AI Action:**
- Explored the senzing directory structure
- Re-discovered reference materials, tools, prompts
- But still didn't know what YOU had done

**Lesson:** AI tools can rediscover the repository, but not your work history.

---

### Recovery Step 2: Verify Tool Access

**Your Prompt:**
```
do you still have access to the senzing mcp server?
```

**AI Response:**
Lists all available Senzing MCP functions:
- `search` - Search for entities by attributes
- `get_entity` - Get full entity details by ENTITY_ID
- `get_source_record` - Get entity by source record ID
- `find_relationship_path` - Find connections
- `expand_entity_network` - Network analysis
- `explain_why_entities_related` - Explain matching logic
- `how_entity_resolved` - Resolution timeline

**Lesson:** Always verify tool access after context loss. Different sessions may have different capabilities.

---

### Recovery Step 3: Locate Work Artifacts

**Your Prompt:**
```
Its already loaded. can you find the snapshot on the watchlist directory and show it to me
```

**AI Action:**
- Searches workspace/watchlist/ directory
- Finds `ftm-watchlist-snapshot-2025-11-14.json`
- Reads the snapshot file

**Lesson:** Reference actual files to restore context. The file system remembers what the AI forgot!

---

### Recovery Step 4: Understand the Snapshot Format

**Your Prompt:**
```
in the senzing tools reference it tells you how to summarize the snapshot, can you do that
```

**AI Action:**
- Consults `SENZING_TOOLS_REFERENCE.md`
- Learns proper snapshot summary format
- Generates correct analysis table

**Lesson:** Reference documentation helps AI understand formats even without prior context.

---

## The Recovered Snapshot Analysis

After recovery, the AI produced this proper summary:

### Entity Resolution Summary by Data Source

| Data Source | Records | Entities | Compression | Cross-Source Matches |
|-------------|---------|----------|-------------|----------------------|
| **CUSTOMERS** | 120 | 75 | 37.5% | 12 |
| **SANCTIONS** | 17 | 14 | 17.6% | 5 |
| **CORP_FILINGS** | 22 | 17 | 22.7% | 10 |
| **TOTAL** | **159** | **92** | **42.1%** | **17** |

### Key Findings

**Overall Compression: 42.1%**
- 159 source records collapsed to 92 unique entities
- 67 records (42%) were duplicates of entities already known

**Cross-Source Matches: 17 entities**
- 5 matches between CUSTOMERS and SANCTIONS (🚨 **watchlist hits!**)
- 8 matches between CUSTOMERS and CORP_FILINGS (customers who are company officers)
- 4 matches between SANCTIONS and CORP_FILINGS (sanctioned individuals with companies)

**Relationships: 12 disclosed relationships**
- Ownership connections (person→company, company→company)
- Directorship connections (person→company with roles)

**Multi-Source Entity: 1**
- One person appears in ALL THREE data sources (customer, sanctioned, company owner)

---

## How to Prevent Context Loss

While you can't always prevent sessions from ending, you can minimize recovery time:

### 1. Document Progress

Create markdown files tracking what you've done:
```bash
# Create a progress log
cat > mapping_progress.md << 'EOF'
# FTM Watchlist Mapping Progress

## Completed Steps
- [x] Generated schema from ftm.jsonl
- [x] Ran 5-stage AI mapping assistant
- [x] Generated mapper code (ftm_mapper.py)
- [x] Validated with linter and analyzer
- [x] Configured SANCTIONS and CORP_FILINGS data sources
- [x] Loaded 39 records successfully
- [x] Took snapshot: ftm-watchlist-snapshot-2025-11-14.json

## Next Steps
- [ ] Analyze snapshot results
- [ ] Investigate multi-source entities
- [ ] Review relationship networks
EOF
```

### 2. Save Key Information

Keep a file with important paths and facts:
```bash
cat > session_context.md << 'EOF'
# Session Context

## Working Directory
/home/ubuntu/workshop/

## Key Files
- Source data: workspace/watchlist/ftm.jsonl
- Schema: workspace/watchlist/ftm_schema.md
- Mapper: ftm_mapper.py
- Output: ftm_senzing.jsonl
- Snapshot: ftm-watchlist-snapshot-2025-11-14.json

## Data Sources Configured
- SANCTIONS (DSRC_ID: 1002)
- CORP_FILINGS (DSRC_ID: 1001)

## Load Results
- 39 records loaded, 0 failed
- 259 candidate matches evaluated
- 5 ambiguous matches
EOF
```

### 3. Reference Past Work

When starting a new session:
```
Read session_context.md and mapping_progress.md to understand
what we've completed. Then help me analyze the snapshot at
workspace/watchlist/ftm-watchlist-snapshot-2025-11-14.json
```

### 4. Use Persistent Artifacts

- Snapshots, logs, output files persist even when context is lost
- Generated code and documentation can be re-read
- File system is your "memory" across sessions

---

## Recovery Strategies Summary

| Strategy | When to Use | How It Helps |
|----------|-------------|--------------|
| **Re-explore repository** | Always first step | Reestablishes project structure |
| **Verify tool access** | When using special capabilities | Confirms what's available |
| **Reference file artifacts** | When work was saved to disk | File system remembers your work |
| **Consult documentation** | When format is unclear | Provides standards and examples |
| **Create context files** | Before session ends | Saves time in next session |

---

## Key Learnings

### Context Loss is Normal
Don't panic when AI doesn't remember previous work. This happens to everyone. Having recovery strategies makes it manageable.

### Documentation > Memory
Files on disk are more reliable than AI memory:
- Progress logs
- Context files
- Generated outputs
- Snapshots and reports

### Incremental Recovery Works
You don't need to redo all the work:
1. Re-establish basic context (explore repo)
2. Verify tools still work
3. Find artifacts from previous work
4. Continue from where you left off

### Prevention is Easier than Recovery
Spending 2 minutes creating a context file saves 20 minutes of recovery later.

---

## Now Back to the Analysis

With context recovered and snapshot properly summarized, let's dig deeper into the interesting findings using the Senzing MCP server!

**[Continue to Step 7: Review with MCP Server →](../67_reviewwithmcp/)**
