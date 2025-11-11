# Workshop Demo Script - For Tomorrow's Presentation

## Opening (2 minutes)

"Today I'm showing you our new **AI-Assisted Data Mapping with Senzing** workshop. This teaches developers how to use AI tools like Amazon Q Developer to map their data into Senzing's entity resolution format using a structured, repeatable workflow."

**Key Innovation:** We're not just teaching people to use AI for code generation - we're teaching them to use the **Senzing Mapping Assistant**, a structured 5-stage workflow that ensures correct, validated mappings every time.

---

## Workshop Overview (3 minutes)

**Navigate to:** Main landing page (http://localhost:1313)

**Point out:**
1. **7 modules, ~2.5-3 hours total**
2. **Self-paced with validation checkpoints**
3. **Complete solutions if you fall behind**
4. **Two datasets: Customers (120 records) + Watchlist (70 entities, bonus)**

**Key Features:**
- ✅ Validation at every step
- ✅ Complete reference solutions
- ✅ Video demonstrations
- ✅ AI-assisted but human-driven
- ✅ Production-ready output

---

## Module Structure Walk-Through (5 minutes)

### Module 1-2: Standard Setup
"Modules 1-2 are standard AWS workshop content - introduction and Cloud9 environment setup with Senzing pre-installed."

### Module 3: Understanding Senzing Mapping
"Module 3 teaches the concepts - the Senzing data model, the 5-stage workflow, and validation tools."

**Key Concepts:**
- Features vs Payload
- Entity types (PERSON vs ORGANIZATION)
- The Senzing Mapping Assistant workflow

### Module 4: Hands-On Customer Mapping ⭐
"This is where the magic happens. Students map real customer data using AI assistance."

**Navigate to Module 4**, show:
- Clear learning objectives
- Materials locations
- 5-stage workflow
- Expected outcomes
- Validation criteria

**The Workflow:**
1. INIT - Load reference files
2. INVENTORY - AI analyzes source schema
3. PLANNING - Determine DATA_SOURCE
4. MAPPING - Disposition each field (Feature or Payload)
5. OUTPUTS - Generate mapper code and documentation

### Module 5: Load and Validate
"After mapping, students load their data into Senzing and see entity resolution in action."

**Show:**
- Senzing tools: sz_configtool, sz_file_loader, sz_snapshot, sz_explorer
- Expected results (120 records → fewer entities due to duplicates)
- Validation checkpoints

### Module 6: Bonus Watchlist
"Advanced students can tackle watchlist data - more complex with nested structures, relationships, and international names."

### Module 7: Cleanup
"Standard cleanup and next steps."

---

## The Complete Solution (10 minutes)

**Navigate to:** File system, show `workshop/solutions/customers/`

### 1. Source Data
```bash
cat workspace/customers/customers.csv | head -5
```
"120 customer records, mix of persons and organizations, realistic data with varying completeness."

### 2. Schema Analysis
```bash
cat solutions/customers/customers_schema.md | head -30
```
"Auto-generated schema showing field statistics, sample values, population percentages."

### 3. Mapping Specification
```bash
cat solutions/customers/customers_mapper.md | head -50
```
"Complete mapping spec - source of truth for how every field maps, with examples and decision rationale."

### 4. Python Mapper
```bash
cat solutions/customers/customers_mapper.py | head -30
```
"Production-ready Python mapper - imports, exports, validates."

### 5. Mapped Output
```bash
wc -l solutions/customers/customers_senzing.jsonl
head -1 solutions/customers/customers_senzing.jsonl | python3 -m json.tool
```
"120 records fully mapped to Senzing format."

---

## Live Validation Demo (5 minutes)

### Run the Linter
```bash
cd workshop/senzing/reference
python3 lint_senzing_json.py ../../solutions/customers/customers_senzing.jsonl
```
**Result:** "OK: All files passed" ✅

### Run the Analyzer
```bash
cd ../tools
python3 sz_json_analyzer.py ../../solutions/customers/customers_senzing.jsonl
```

**Point out in output:**
- GREEN = MAPPED (Senzing recognizes)
  - All features correctly identified
  - 120 records, 100% coverage on required fields
  - Identifiers: SSN, DRLIC, PASSPORT, NATIONAL_ID all working
- YELLOW = UNMAPPED (Payload attributes)
  - CUSTOMER_SINCE_DATE, ACCOUNT_STATUS, ACCOUNT_BALANCE, CUSTOMER_TIER
  - Correctly excluded from matching
- RED = ERROR
  - DATA_SOURCE not registered yet (expected - would be added in Module 5)
- ORANGE = WARNINGS
  - Sparse optional fields (normal for real data)

"This proves our mapping is 100% correct and ready to load."

---

## The Secret Sauce: Complete Conversation Log (5 minutes)

**Navigate to:** `solutions/customers/workshop_process.md`

```bash
cat solutions/customers/workshop_process.md | head -100
```

**Explain:**
"This is the complete conversation between the developer and the AI. Every prompt, every decision, every validation step - all documented. This becomes our video script."

**Show key moments:**
1. Loading the mapping assistant
2. AI asking for DATA_SOURCE
3. The REGISTRATION_DATE → CUSTOMER_SINCE_DATE decision
   - "First AI said use REGISTRATION_DATE (Senzing feature)"
   - "User caught it - this is customer signup, not incorporation"
   - "Renamed to avoid parser confusion"
   - "This shows iterative refinement with AI"
4. Final validation with linter and analyzer

"This isn't just code generation - this is AI-assisted decision-making with validation at every step."

---

## Next Steps & Timeline (2 minutes)

### What's Complete NOW:
- ✅ All workshop modules structured
- ✅ Module 4 (customer mapping) 100% complete with solutions
- ✅ Validation tools tested and working
- ✅ Complete conversation log ready to become video
- ✅ Bonus watchlist data prepared

### Next Steps:
1. **Record Module 4 video** (use workshop_process.md as script) - 1 hour video
2. **Record Module 5 video** (load and validate) - 30 minutes
3. **Fill in Module 3 content** (concepts and theory)
4. **Optional: Module 6 watchlist video**

**Timeline:**
- Core workshop (Modules 1-5): Ready in 1-2 weeks after video recording
- Bonus module (Module 6): Can be added later

---

## Value Proposition (2 minutes)

### For AWS:
- Showcases Amazon Q Developer for complex technical workflows
- Real production use case (data mapping for entity resolution)
- Validates AI-assisted development with linting and analysis

### For Senzing:
- Makes data mapping accessible to more developers
- Reduces time from source data to loaded entities
- Teaches best practices through structured workflow

### For Developers:
- Learn AI-assisted workflow (not just code generation)
- Understand entity resolution concepts
- Get production-ready mapper code
- Validate correctness at every step

---

## Q&A Prep

### Q: "How is this different from just asking AI to write a mapper?"
**A:** "The Senzing Mapping Assistant is a structured 5-stage workflow with validation gates. The AI guides you through decisions, but YOU choose how to map based on understanding your data. Every output is validated with linting and analysis tools. This teaches correct mapping, not just code generation."

### Q: "What if students get stuck?"
**A:** "Every module has complete reference solutions. If you fall behind, copy the solution files and continue. The workshop is designed to let you catch up at any checkpoint."

### Q: "How long does it take to complete?"
**A:** "Core workshop (Modules 1-5): 2.5 hours. Bonus watchlist: Add 45 minutes. Self-paced, so students can take breaks."

### Q: "What AI tools work?"
**A:** "Amazon Q Developer is recommended and what we'll demo. Any AI with Claude 3.5 Sonnet or better should work. The Mapping Assistant prompt is AI-agnostic."

### Q: "Is this production-ready?"
**A:** "Yes! The customer mapping produces 120 validated records ready to load into Senzing. All validation tools pass. Students learn the exact workflow they'd use for their own data."

---

## Closing

"This workshop is ready to demonstrate and teach today. Module 4 is production-ready with complete solutions. Modules 5-6 need video walkthroughs which we can record using the existing materials. This represents a new approach to teaching data integration - not just AI code generation, but AI-assisted decision-making with structured validation."

**Call to Action:** "Let me know if you'd like to see any specific part in more detail, or if you're ready for me to start recording the video demonstrations."
