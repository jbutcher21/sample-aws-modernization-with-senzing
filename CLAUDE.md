# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is an **AWS Workshop for AI-Assisted Entity Resolution Mapping with Senzing**. The workshop teaches developers how to map their data into Senzing's entity resolution format using AI tools like Amazon Q Developer with a structured 5-stage workflow called the **Senzing Mapping Assistant**.

**Key Concepts:**
- **Entity Resolution**: Identifying records that refer to the same real-world entity across datasets
- **Senzing**: Entity resolution engine that requires JSON format with specific features (NAME, ADDRESS, identifiers, etc.)
- **AI-Assisted Mapping**: Using AI to help map source data fields to Senzing features, with human validation at each step

## Development Commands

### Local Development (Hugo)

```bash
# Start local development server
hugo server -D

# View at: http://localhost:1313/

# Build static site
hugo -D -d public

# Check Hugo version
hugo version
```

### Git Submodules (Hugo Theme)

```bash
# Initialize and update submodules (required after clone)
git submodule init
git submodule update

# Full recursive update if needed
git submodule update --init --recursive
```

### Working with Workshop Materials

All workshop materials are in the `workshop/` directory:

```bash
# Validate Senzing JSON output
python3 workshop/senzing/reference/lint_senzing_json.py <file.jsonl>

# Analyze mapped data (shows which fields are recognized)
python3 workshop/senzing/tools/sz_json_analyzer.py <file.jsonl>

# Generate schema from CSV
python3 workshop/senzing/tools/sz_schema_generator.py <file.csv>

# Run mapper (example)
python3 workshop/solutions/customers/customers_mapper.py \
  workshop/workspace/customers/customers.csv \
  -o output.jsonl
```

## Repository Structure

### Content Organization (`content/`)

Hugo workshop content organized by modules:

1. **Module 1** (`1_ModuleOne/`) - Introduction to workshop
2. **Module 2** (`2_EnvironmentSetup/`) - AWS Cloud9 environment setup with Senzing
3. **Module 3** (`3_UnderstandingMapping/`) - Senzing concepts, data model, mapping workflow
4. **Module 4** (`4_HandsOnMapping/`) - **Core module**: Hands-on customer data mapping with AI
5. **Module 5** (`5_LoadAndValidate/`) - Loading mapped data into Senzing, viewing results
6. **Module 6** (`6_BonusWatchlist/`) - Advanced: Mapping watchlist data with relationships
7. **Module 7** (`7_Cleanup/`) - Cleanup and next steps

### Workshop Materials (`workshop/`)

```
workshop/
├── workspace/              # Source data for students
│   ├── customers/          # Customer CSV (120 records)
│   └── watchlist/          # Watchlist JSON (70 entities)
├── solutions/              # Complete reference implementations
│   ├── customers/          # Full customer mapping solution
│   │   ├── customers_mapper.py         # Production mapper
│   │   ├── customers_mapper.md         # Mapping specification
│   │   ├── customers_schema.md         # Schema analysis
│   │   ├── customers_senzing.jsonl     # Mapped output
│   │   └── workshop_process.md         # Complete AI conversation log
│   └── watchlist/          # Watchlist mapping (bonus)
└── senzing/                # Senzing resources
    ├── prompts/            # Senzing Mapping Assistant prompt
    ├── reference/          # Entity spec, examples, linter, crosswalks
    └── tools/              # Schema generator, JSON analyzer
```

### Configuration Files

- `config.toml` - Hugo site configuration (title, theme, menu shortcuts)
- `webspec.yml` - AWS CodeBuild spec for automated deployment
- `.gitmodules` - Hugo theme submodule (hugo-theme-learn)

## Architecture and Key Concepts

### The Senzing Mapping Assistant Workflow

This is the core pedagogical innovation of the workshop. A 5-stage AI-assisted process:

**STAGE 1: INIT**
- Load reference files (`senzing_entity_specification.md`, examples, crosswalks)
- Verify tools are available

**STAGE 2: INVENTORY**
- AI analyzes source data schema
- Extract all fields with data types and sample values

**STAGE 3: PLANNING**
- Determine DATA_SOURCE code (e.g., "CUSTOMERS")
- Identify entity types (PERSON vs ORGANIZATION)

**STAGE 4: MAPPING**
- For each field, decide: Feature (for matching) or Payload (operational data)
- Map Features to Senzing attributes (NAME, ADDRESS, identifiers, etc.)
- Keep Payload attributes as-is for later retrieval

**STAGE 5: OUTPUTS**
- Generate mapper Python script
- Generate mapping documentation
- Generate mapped JSONL output
- Validate with linter and analyzer

### Senzing JSON Format

**Features** - Used for entity resolution matching:
- Names: `NAME_FIRST`, `NAME_LAST`, `NAME_ORG`
- Addresses: `ADDR_LINE1`, `ADDR_CITY`, `ADDR_STATE`, `ADDR_POSTAL_CODE`
- Identifiers: `SSN_NUMBER`, `DRIVERS_LICENSE_NUMBER`, `PASSPORT_NUMBER`
- Demographics: `DATE_OF_BIRTH`, `GENDER`
- Contact: `PHONE_NUMBER`, `EMAIL_ADDRESS`

**Payload Attributes** - Operational data not used for matching:
- Custom fields like `CUSTOMER_SINCE_DATE`, `ACCOUNT_STATUS`
- Stored with entity but don't influence resolution

**Required Fields:**
- `DATA_SOURCE` - Origin system identifier (must be uppercase)
- `RECORD_ID` - Unique ID within data source
- `RECORD_TYPE` - PERSON or ORGANIZATION (optional but recommended)

### Validation Tools

**lint_senzing_json.py**
- Checks JSON syntax validity
- Verifies required fields present
- Reports errors by line number

**sz_json_analyzer.py**
- Shows which attributes are recognized by Senzing (GREEN)
- Shows unmapped payload attributes (YELLOW)
- Shows errors like unregistered DATA_SOURCE (RED)
- Shows warnings for sparse fields (ORANGE)

## Hugo Theme

This workshop uses the **hugo-theme-learn** theme (git submodule in `themes/`).

**Special Shortcodes Used:**
- `{{% notice tip %}}` - Blue tip boxes
- `{{% notice info %}}` - Light blue info boxes
- `{{% notice warning %}}` - Orange warning boxes
- `{{% notice note %}}` - Gray note boxes

**Front Matter:**
- `title` - Page title
- `chapter: true` - Makes it a chapter landing page
- `weight` - Controls menu ordering
- `draft: false` - Published (omit `-D` flag requirement)

## Common Development Patterns

### Adding Content to Modules

Each module is in `content/N_ModuleName/`:
1. Create `_index.md` for module landing page with `chapter: true`
2. Create numbered subpages: `21_FirstStep.md`, `22_SecondStep.md`, etc.
3. Use `weight` in front matter for ordering

### Working with Solutions

Solutions in `workshop/solutions/` are complete reference implementations:
- Students can catch up at any checkpoint by copying solution files
- Each solution includes README explaining the mapping
- `workshop_process.md` contains complete AI conversation logs (video script material)

### Testing Workshop Locally

1. Start Hugo server: `hugo server -D`
2. Navigate through modules at `http://localhost:1313`
3. Test navigation, code blocks, shortcodes
4. Verify images load from `static/` directory

### Deployment

Automated via AWS CodeBuild using `webspec.yml`:
1. Install Hugo
2. Initialize submodules
3. Build with `hugo -D -d public`
4. Sync to S3 bucket
5. Invalidate CloudFront cache

## Important Notes

### Workshop Pedagogy

- **Self-paced with validation checkpoints**: Students validate at each stage
- **Complete solutions provided**: Students can catch up if they fall behind
- **AI-assisted but human-driven**: AI guides decisions, humans make final calls
- **Production-ready outputs**: Mapped data passes all validation tools

### Data Files

**Customers** (120 records):
- Mix of PERSON (114) and ORGANIZATION (6) records
- 19 fields including identifiers (SSN, driver's license, passport, national ID)
- Realistic data with varying completeness

**Watchlist** (70 entities - bonus module):
- FollowTheMoney (FTM) format with nested structures
- International names, relationships, sanctions
- More complex than customers

### Common Mistakes to Avoid

1. **REGISTRATION_DATE confusion**: In source data, avoid naming dates `REGISTRATION_DATE` as Senzing reserves this for legal incorporation dates. Use names like `CUSTOMER_SINCE_DATE` instead.

2. **DATA_SOURCE must be uppercase**: Senzing requirement, enforced by tools.

3. **Submodules not initialized**: Theme won't load if `git submodule update --init` not run after clone.

4. **Draft content**: Use `-D` flag with Hugo to include draft pages during development.

## Workshop Status

**Production-Ready:**
- Module 4 (Customer Mapping) - Complete with solutions, validation tools tested
- All module structures created
- Complete customer mapping solution with conversation logs

**In Progress:**
- Video demonstrations for Modules 4-5 (scripts exist in `workshop_process.md`)
- Module 3 detailed content (structure exists)
- Module 6 watchlist walkthrough (bonus, can be added later)

## References

- Hugo Learn Theme: https://learn.netlify.app/
- Markdown Syntax: https://learn.netlify.app/en/cont/markdown/
- AWS Workshop Studio: https://awsworkshop.io
- Senzing documentation embedded in `workshop/senzing/reference/`
