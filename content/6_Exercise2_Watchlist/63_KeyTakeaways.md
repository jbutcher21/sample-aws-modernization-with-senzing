+++
title = "Key Takeaways"
weight = 63
+++

## What You've Accomplished

Congratulations! If you completed both exercises, you've progressed from guided step-by-step mapping to self-directed complex data workflows.

### Exercise Comparison

| Aspect | Exercise 1: Customers | Exercise 2: Watchlist |
|--------|----------------------|----------------------|
| **Data Format** | Simple CSV | Nested JSON |
| **Approach** | Step-by-step with screenshots | Self-guided with outcomes |
| **Language** | English only | Multi-language (Cyrillic, Arabic, Latin) |
| **Structure** | Flat, one-to-one | Hierarchical with dependencies |
| **Relationships** | None | Ownership, Directorship networks |
| **Processing** | Single-pass | Multi-pass with merge strategy |
| **AI Interaction** | Follow guided steps | Question assumptions, direct workflow |

---

## New Skills from Exercise 2

### 1. Taking Charge of AI Workflows

**Exercise 1:** You followed along as AI guided each step.

**Exercise 2:** You directed the AI, questioned assumptions, and made critical decisions:
- Verified identifier types against actual data (not just schema)
- Discovered missing company relationships AI initially overlooked
- Corrected NAME_ORG conventions before they impacted matching
- Made final calls on field dispositions

**Key Lesson:** AI is a knowledgeable assistant, not an autonomous agent. Your domain expertise and critical evaluation produce quality results.

---

### 2. Multi-Pass Processing for Complex Data

**The Challenge:** FTM data has dependencies - Sanction records reference Person IDs that must exist first.

**The Solution:**
- **Pass 1:** Create master entities (Person, Company)
- **Pass 2:** Merge metadata (Sanctions as payload)
- **Pass 3:** Add relationships (Ownership, Directorship as REL_POINTER)

**Key Lesson:** When source data has references and dependencies, identify what must exist first, then process in the correct order.

---

### 3. Managing AI Context

**The Challenge:** Long interactive mapping sessions consume AI context (token limits). You need to ask questions for quality, but conversations can't be infinite.

**Be Concise:**
- Ask specific questions: "Are you sure those are all the identifier types?" ✓
- Avoid open-ended requests: "Tell me everything about identifiers" ✗
- Get to the point: "How do you know?" vs "Can you explain your reasoning in detail?"

**Accept Compact Offers:**
- When AI warns context ~80% full and offers to compact, **say YES**
- Compact compresses conversation history to free tokens
- Lets you continue in the same session with context preserved
- At 100%, session resets automatically - no choice, context lost

**Recovering After Context Loss:**
- Use `@senzing` to reload reference files
- Check workspace for generated artifacts (mapper.py, schema.md, output.jsonl)
- Tell AI where you left off: "Data is already loaded, find the snapshot file"
- Reference specific files to rebuild context quickly

**Key Lesson:** Balance quality (ask questions) with efficiency (be concise, accept compacts). If context resets, artifacts and clear directions get you back on track.

---

### 4. Cross-Language Entity Resolution

**What You Saw:** Senzing matched Alexander Vasiliev across:
- Belarusian Cyrillic: "ВАСІЛЬЕЎ Аляксандр Паўлавіч"
- Russian Cyrillic: "ВАСИЛЬЕВ Александр Павлович"
- English/Latin: "Alexander Pavlovich Vasiliev"

Plus international phone formats and transliteration variants.

**Key Lesson:** Map international data faithfully as-is. Don't pre-normalize. Senzing's algorithms handle character set variations, transliterations, and format differences automatically.

---

### 5. Relationship Networks Reveal Hidden Patterns

**Discovery:** Entity resolution identified Alexander Vasiliev in all three data sources (CUSTOMERS, SANCTIONS, CORP_FILINGS), revealing:
```
Vasiliev (Russia/Belarus) → OWNS → Mullenkrants (Germany) → EMPLOYS → Siddiqui (Pakistan)
```

This multi-jurisdictional network showed a sanctioned individual controlling a company with another sanctioned person in management.

**Key Lesson:** REL_POINTER relationships combined with entity resolution reveal networks and patterns that single-source or relationship-free analysis misses entirely.

---

### 6. Validation is Multi-Layered

Each validation tool catches different issues:
- **Linter:** JSON syntax, structure, required fields
- **Analyzer:** Data source configuration, Senzing feature recognition
- **Loader:** Actual processing, candidate matching
- **Snapshot:** Resolution quality, compression rates, cross-source matches

**Key Lesson:** Run all validation tools in sequence. Skipping any layer means missing issues that could have been caught earlier and more cheaply.

---

## Combined Skills from Both Exercises

After completing both exercises, you now have:

**✅ Foundation Skills (Exercise 1)**
- Understand the 5-stage Senzing Mapping Assistant workflow
- Can distinguish Features (for matching) from Payload (operational data)
- Know how to use validation tools (linter, analyzer)
- Can interpret entity resolution results (snapshots, compression)
- Can investigate entities using MCP server

**✅ Advanced Skills (Exercise 2)**
- Can handle complex nested data with dependencies
- Know when and how to use multi-pass processing
- Can work with international data and character sets
- Can map entity relationships using REL_POINTER
- Can direct AI workflows and question assumptions
- Can manage AI context and recover from session issues

**✅ Production-Ready Capabilities**
- Map any data source (CSV, JSON, or other) to Senzing format
- Validate mappings thoroughly before production use
- Analyze entity resolution results to identify high-value findings
- Work effectively with AI tools while maintaining control

---

## Next Steps: Apply to Your Own Data

You're now ready to map your own data sources. Here's how to get started:

### 1. Start with the Workflow

Use the 5-stage Mapping Assistant workflow from Exercise 2:
1. **INIT:** Load reference files (@senzing)
2. **INVENTORY:** Extract and categorize all source fields
3. **PLANNING:** Identify entity types, data sources, processing strategy
4. **MAPPING:** Map each field to Features, Payload, or Ignored
5. **OUTPUTS:** Generate mapper code and documentation

### 2. Choose Your Approach

**Simple data (like Exercise 1 CSV):**
- Single-pass processing
- One entity type per record
- Follow guided workflow

**Complex data (like Exercise 2 JSON):**
- Multi-pass processing if there are dependencies
- Question AI assumptions actively
- Verify decisions against actual data
- Use outcome checkpoints to stay on track

### 3. Validate Thoroughly

Run all validation tools in sequence:
```bash
# 1. Lint for syntax
python3 senzing/tools/lint_senzing_json.py your_output.jsonl

# 2. Analyze for coverage
python3 senzing/tools/sz_json_analyzer.py your_output.jsonl -o analysis.md

# 3. Load and check errors
sz_file_loader -f your_output.jsonl

# 4. Snapshot for quality
sz_snapshot -o your_snapshot.json -Q
```

### 4. Iterate and Improve

- Review compression rates (30-50% is healthy)
- Check for cross-source matches
- Use MCP server to investigate interesting entities
- Refine mappings based on results

---

## Remember

**Entity resolution is both science and art:**
- **Science:** Structured workflows, validation pipelines, algorithms
- **Art:** Field disposition decisions, recognizing data quality issues, interpreting results

**AI assistance accelerates both:**
- Speeds up the science (faster mapping, fewer syntax errors)
- Augments the art (suggests patterns, explains logic)
- Never replaces human judgment

Your domain knowledge + AI's Senzing expertise = Quality results

---

::alert[
**Workshop Complete!** You've learned AI-assisted entity resolution from foundations to advanced techniques. Now apply these skills to your own data challenges. Good luck!
]{type="info"}
