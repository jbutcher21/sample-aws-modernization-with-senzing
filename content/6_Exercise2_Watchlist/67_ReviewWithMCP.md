+++
title = "Step 7: Review with MCP Server"
weight = 67
+++

## Deep Entity Investigation Using Senzing MCP

Now that context is recovered and you understand the snapshot results, use the Senzing MCP server to investigate specific entities, relationships, and resolution logic.

::alert[**MCP Server Advantage**: While snapshots give you statistics, the MCP server lets you ask "how" and "why" questions about specific entities and matches. This is where AI-assisted analysis really shines!]{type="warning"}

---

## Investigation 1: The Multi-Source Entity

The snapshot showed **1 entity spans all three data sources**. Let's find it and understand how it came together.

### Prompt
```bash
Show me the entity that appears in all three data sources (CUSTOMERS, SANCTIONS, CORP_FILINGS)
```

### AI Response

**Entity ID: 91**
**Resolved Name:** ВАСІЛЬЕЎ Аляксандр Паўлавіч (Alexander Pavlovich Vasiliev)

#### Source Records (3)

**1. CUSTOMERS:2063** - Alexander Pavlovich Vasiliev
- **Status:** Platinum customer since 2023
- **Contact:** 481-285-6234, avasiliev@example.com
- **Address:** Smolensk, Russia

**2. SANCTIONS:corp-filings-person-2062** - ВАСИЛЬЕВ Александр Павлович
- **Program:** SANCTIONS
- **Authority:** Sanctions Authority
- **Reason:** Category: Arms Trafficking
- **Listing Date:** 2014-03-17
- **Status:** Active
- **Phone:** (4812)85-62-34

**3. CORP_FILINGS:sanctions-person-2061** - ВАСІЛЬЕЎ Аляксандр Паўлавіч
- **Ownership:** 100% owner of Mullenkrants Autoworks
- **Country:** Belarus
- **Phone:** +7(4812)85-62-34

#### Resolved Features

**Names (3 variants):**
- English: "Alexander Pavlovich Vasiliev"
- Russian (Cyrillic): "ВАСИЛЬЕВ Александр Павлович"
- Belarusian (Cyrillic): "ВАСІЛЬЕЎ Аляксандр Паўлавіч"

**Phone Numbers (3 formats):**
- US format: "481-285-6234"
- Russian format: "(4812)85-62-34"
- International format: "+7(4812)85-62-34"

**Relationships:**
- Owns Mullenkrants Autoworks GmbH (100%)

::alert[**Critical Finding**: A Platinum customer is on the sanctions list for arms trafficking! This is exactly the kind of hidden risk entity resolution reveals.]{type="error"}

---

## Investigation 2: Resolution Timeline

Understanding **how** this entity came together reveals Senzing's cross-language and international format handling.

### Prompt
```bash
how did this entity come together
```

### AI Response: Step-by-Step Resolution

The MCP server's `how_entity_resolved()` function shows the complete timeline:

#### Step 1: CORP_FILINGS + SANCTIONS Match

**Match Key:** +NAME+PHONE (Rule: CNAME_CFF - Close Name, Close Features First)

**NAME Match (Score: 90)**
- **CORP_FILINGS:** "ВАСІЛЬЕЎ Аляксандр Паўлавіч" (Belarusian Cyrillic)
- **SANCTIONS:** "ВАСИЛЬЕВ Александр Павлович" (Russian Cyrillic)
- **Why matched:** Cyrillic name transliteration variance (Belarusian vs Russian)
  - ВАСІЛЬЕЎ ↔ ВАСИЛЬЕВ (different Cyrillic spelling of same name)
  - Same underlying person, different script conventions

**PHONE Match (Score: 90)**
- **CORP_FILINGS:** "+7(4812)85-62-34"
- **SANCTIONS:** "(4812)85-62-34"
- **Why matched:** Same Russian phone number, different formatting
  - +7 is Russia country code
  - (4812) is Smolensk area code
  - 85-62-34 is local number

**Resolution Decision:** DEFINITIVE MATCH → Merged into Entity 91

---

#### Step 2: CUSTOMERS Added to Merged Group

**Match Key:** +NAME+PHONE (Rule: CNAME_CFF)

**NAME Match (Score: 90)**
- **Existing entity:** "ВАСІЛЬЕЎ Аляксандр Паўлавіч" + "ВАСИЛЬЕВ Александр Павлович"
- **CUSTOMERS:** "Alexander Pavlovich Vasiliev"
- **Why matched:** Cyrillic to Latin transliteration
  - ВАСІЛЬЕЎ / ВАСИЛЬЕВ → Vasiliev (standard transliteration)
  - Аляксандр / Александр → Alexander (Belarusian/Russian to English)
  - Паўлавіч / Павлович → Pavlovich (patronymic transliteration)

**PHONE Match (Score: 98)**
- **Existing entity:** "+7(4812)85-62-34" and "(4812)85-62-34"
- **CUSTOMERS:** "481-285-6234"
- **Why matched:** Normalized phone equivalence
  - +7 (Russia) dropped
  - (4812) area code → 4812
  - Dashes vs parentheses vs plus signs normalized
  - Core digits: 4812-85-62-34 match across all formats!

**Resolution Decision:** DEFINITIVE MATCH → Added to Entity 91

---

### Key Insights from Timeline

**1. Cross-Language Matching Works**
Senzing successfully matched:
- Belarusian Cyrillic ↔ Russian Cyrillic
- Cyrillic ↔ Latin transliteration
- Different name conventions across cultures

**2. International Phone Format Normalization**
Three phone number formats recognized as identical:
- US-style digits: 481-285-6234
- Russian style: (4812)85-62-34
- International: +7(4812)85-62-34

**3. Incremental Resolution**
Entity built in steps:
1. First match: CORP_FILINGS + SANCTIONS (both Cyrillic)
2. Second match: Adding CUSTOMERS (Latin) to existing Cyrillic names

**4. High-Confidence Matches**
All matches scored 90+ (out of 100), indicating strong evidence:
- Multiple features agreed (name + phone)
- Patterns consistent with known transliteration rules
- No conflicting information

---

## Investigation 3: Relationship Network

Now let's map out the corporate structure and relationships.

### Prompt
```bash
show his relationships in a simple graph view
```

### AI Response: Network Visualization

```
Entity 91 (Alexander Pavlovich Vasiliev)
    │
    │ OWNS 100%
    ▼
Entity 90 (Mullenkrants Autoworks GmbH)
    │ Location: Germany
    │ Industry: Automotive Manufacturing
    │
    │ PRESIDENT
    ▼
Entity 100014 (Faisal Siddiqui)
    │ Location: Pakistan
    │ Status: Customer + Sanctioned
```

### Network Analysis

**Multi-Jurisdictional Network:**
- **Russia/Belarus** → **Germany** → **Pakistan**
- Person (Russia/Belarus) owns company (Germany)
- Company employs sanctioned person (Pakistan)

**All Parties Sanctioned:**
- Alexander Vasiliev: Arms Trafficking (2014)
- Mullenkrants Autoworks: Company owned by sanctioned individual
- Faisal Siddiqui: Category unknown (requires investigation)

**Corporate Structure:**
- Clear ownership: 100% stake (not partial or joint)
- Management hierarchy: President role defined
- Cross-border operations: Multiple countries involved

**Risk Implications:**
- Sanctioned individual controls entire company
- Company may be shell corporation or front
- International network suggests sophisticated operation
- Second sanctioned individual in management raises red flags

::alert[**Compliance Impact**: This network would trigger enhanced due diligence requirements:
- Know Your Customer (KYC) violations
- Anti-Money Laundering (AML) concerns
- Sanctions compliance issues
- Potential need to freeze accounts and report to authorities]{type="warning"}

---

## Investigation 4: Understanding Match Logic

For any two entities, you can ask Senzing to explain the matching logic.

### Prompt
```bash
explain why Entity 91 and Entity 90 are related
```

### AI Response

**Relationship Type:** REL_POINTER (disclosed relationship, not inferred match)

**Source:** Ownership record from FTM data
- **Owner:** Alexander Vasiliev (Entity 91)
- **Asset:** Mullenkrants Autoworks (Entity 90)
- **Percentage:** 100%
- **Role:** OWNER_OF

**Not a Resolved Match:**
This is a **declared relationship** from source data, not a match Senzing discovered. The FTM Ownership record explicitly stated this ownership structure.

**Why This Matters:**
- REL_POINTER relationships come from your data
- Senzing preserves and indexes them for network analysis
- Different from entity resolution matches (which Senzing infers)

---

## Common Investigation Patterns

### Finding Watchlist Hits
```bash
Show me all entities that have both CUSTOMERS and SANCTIONS records
```
Returns entities that are both customers and on watchlists - high-priority review cases.

### Exploring Networks
```bash
expand network from Entity 91 showing all relationships up to 2 degrees
```
Shows complete network including indirect connections.

### Understanding Specific Matches
```bash
explain why entity 91 matched with CUSTOMERS:2063
```
Shows exact features and scores that led to the match.

### Finding Ambiguous Cases
```bash
show me entities with ambiguous matches that need review
```
Lists cases where Senzing found multiple possible matches requiring human judgment.

---

## Key Learnings

### MCP Server Enables Deep Analysis
- Snapshots give you statistics
- MCP lets you investigate **specific cases**
- You can ask "how" and "why" questions about resolution logic

### Cross-Language Resolution is Powerful
Senzing handled:
- Cyrillic script variations (Belarusian vs Russian)
- Cyrillic ↔ Latin transliteration
- International phone format differences

This works because Senzing:
- Normalizes data to standard forms
- Uses phonetic encoding for names
- Applies international format standards

### Relationships Tell Stories
The network graph revealed:
- Multi-jurisdictional corporate structure
- Connections between sanctioned individuals
- Potential shell corporation patterns
- Compliance risk indicators

### Resolution Timelines Show Logic
Understanding **how** entities merged helps you:
- Validate that matches make sense
- Identify potential false positives
- Explain results to stakeholders
- Tune matching rules if needed

---

## Next Steps

You've now completed the full watchlist mapping and analysis workflow! The final step is to reflect on key takeaways and lessons learned.

**[Continue to Step 8: Key Takeaways →](../68_keytakeaways/)**
