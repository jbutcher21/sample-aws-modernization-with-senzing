# Quick Start - Demo Tomorrow

## Run the Workshop Site

```bash
cd sample-aws-modernization-with-senzing
hugo server
```

Then open: http://localhost:1313

## Demo Files

- **DEMO_SCRIPT.md** - Complete presentation script (30 min demo)
- **WORKSHOP_STATUS.md** - What's done, what's needed
- This file - Quick commands

## Quick Validation Demo

```bash
# Change to workshop directory
cd sample-aws-modernization-with-senzing/workshop

# Show source data
head -5 workspace/customers/customers.csv

# Show mapped output
head -1 solutions/customers/customers_senzing.jsonl | python3 -m json.tool

# Run linter (should pass)
python3 senzing/reference/lint_senzing_json.py solutions/customers/customers_senzing.jsonl

# Run analyzer (shows what Senzing recognizes)
python3 senzing/tools/sz_json_analyzer.py solutions/customers/customers_senzing.jsonl
```

## Key Stats to Mention

- **120 customer records** mapped successfully
- **114 persons + 6 organizations** (mixed entity types)
- **19 source fields** → 15 Senzing features + 4 payload attributes
- **100% validation passed** (linter + analyzer)
- **4 identifier types** mapped: SSN, DRLIC, PASSPORT, NATIONAL_ID
- **Complete conversation log** ready for video: `solutions/customers/workshop_process.md`

## Workshop Structure

1. **Module 1:** Introduction (10 min)
2. **Module 2:** Environment Setup (15 min)
3. **Module 3:** Understanding Mapping (30 min)
4. **Module 4:** ⭐ Hands-On Customer Mapping (60 min) - **COMPLETE**
5. **Module 5:** Load and Validate (30 min) - **Structure ready**
6. **Module 6:** Bonus Watchlist (Optional) - **Prepared**
7. **Module 7:** Cleanup (10 min)

## What's Ready TODAY

✅ Complete customer mapping solution
✅ All validation tools working
✅ Complete AI conversation log
✅ Watchlist data prepared
✅ Workshop structure complete
✅ Demo scripts written

## What Needs Video

📹 Module 4 walkthrough (use workshop_process.md as script)
📹 Module 5 load/validate demo
📹 Module 6 watchlist (optional, can add later)

## The Innovation

**Not just AI code generation** - this teaches:
- Structured 5-stage workflow (Senzing Mapping Assistant)
- Decision-making with AI guidance
- Validation at every step
- Production-ready output

## Questions?

See DEMO_SCRIPT.md for full presentation with Q&A prep.
