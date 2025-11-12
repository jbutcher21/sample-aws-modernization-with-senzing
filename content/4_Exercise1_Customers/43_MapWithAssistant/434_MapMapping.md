---
title: "Stage 4: MAPPING"
weight: 434
---

## Stage 4: MAPPING - Field-by-Field Decisions

This is the core of the mapping process. The AI will present how each field maps to Senzing.

![MAPPING stage - Field mappings](/images/exercise1/3-mapping6.png)

For each field, the AI shows:
- **Senzing feature** (for matching) or **Payload attribute** (for storage only)
- **Special processing** (parsing, transformations, etc.)
- **Citation** - Which section of the spec justified this decision
- **Confidence** - How certain the AI is about this mapping

{{% notice warning %}}
**Review Carefully:** Don't blindly accept the mappings. The AI cites its reasoning, but you must validate each decision based on your business requirements and data quality.
{{% /notice %}}

### Ask Questions About Mappings

After presenting all mappings, the AI gives you a chance to ask questions:

![MAPPING stage - Question opportunity](/images/exercise1/3-mapping7.png)

**Example questions to consider:**

**Question 1: Name Parsing**

**Ask Amazon Q:** `Should we really be parsing those names and what will it do on organizations?`

![Name parsing explanation](/images/exercise1/3-mapping8.png)

**Question 2: Address Mapping**

**Ask Amazon Q:** `Why did you map to ADDR_FULL rather than ADDR_LINE1?`

![Address mapping explanation](/images/exercise1/3-mapping9.png)

**Question 3: Understanding Payload**

**Ask Amazon Q:** `So what is payload and why did you map those fields to it?`

![Payload explanation - part 1](/images/exercise1/3-mapping10.png)

![Payload explanation - part 2](/images/exercise1/3-mapping11.png)

### Handle Mapping Issues

The AI may identify potential problems. For example, REGISTRATION_DATE has special meaning in Senzing:

**Ask Amazon Q:** `What does the spec say about REGISTRATION_DATE?`

![REGISTRATION_DATE issue identified](/images/exercise1/3-mapping12.png)

![REGISTRATION_DATE options](/images/exercise1/3-mapping13.png)

**Make your choice:**

**Ask Amazon Q:** `I choose B, but what shall we call it?`

![Suggested alternative name](/images/exercise1/3-mapping14.png)

**Tell Amazon Q:** `Call it CUSTOMER_SINCE`

The AI will regenerate the full mapping table with your changes and ask if you're ready to proceed.

**Tell Amazon Q:** `Yes`

---

## Validate Sample Records with the Linter

Before generating the final code, the AI will create sample JSON records and validate them with the linter to ensure the mapping is correct.

**Tell Amazon Q:** `OK to proceed`

{{% notice warning %}}
**Security Approval Required:** The AI will ask permission to run the Python linter script. Always review what the AI wants to run before approving.
{{% /notice %}}

The AI will:
1. Generate sample Senzing JSON records based on your mappings
2. Run the linter to validate JSON structure and required fields
3. Self-correct if errors are found
4. May ask you questions if it encounters ambiguous issues

**What to expect during validation:**

- **Errors are rare** - And are usually handled without needing guidance.
- **Self-correction** - Watch as the AI identifies issues, explains what's wrong, and fixes them
- **Questions** - The AI may ask you to clarify field meanings or choose between options
- **You can intervene** - Press Escape to stop and ask "What are you doing?" or "What does the entity spec say about [field]?"

{{% notice note %}}
**Catch Mistakes Here:** If we hadn't caught the REGISTRATION_DATE issue earlier, the AI would have found it here during validation and asked you to resolve it. The linter is your safety net!
{{% /notice %}}

When validation succeeds:

![Sample validation successful](/images/exercise1/3-mapping15.png)

**Tell Amazon Q:** `Yes`

{{% notice info %}}
**Checkpoint:** The AI should have successfully validated sample JSON records with the linter. If there were errors, they should have been resolved before proceeding to generate the final mapper code.
{{% /notice %}}
