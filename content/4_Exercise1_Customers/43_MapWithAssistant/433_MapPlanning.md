---
title: "Stage 3: PLANNING"
weight: 433
---

## Stage 3: PLANNING - High-Level Strategy

The AI automatically moves to planning and presents a high-level mapping strategy.

![PLANNING stage - Mapping strategy](/images/exercise1/3-mapping4.png)

The AI will:
- Suggest a DATA_SOURCE name (you can change this)
- Identify entity types (PERSON vs ORGANIZATION)
- Explain how it will handle special cases (like dynamic identifiers)

**Understanding key concepts:**

If you see unfamiliar terms, ask about them! For example:

**Ask Amazon Q:** `What is that dynamic identifier handling?`

![PLANNING stage - Explaining dynamic identifiers](/images/exercise1/3-mapping5.png)

{{% notice info %}}
**Dynamic Identifiers:** Many source systems use codes for identifier types (e.g., "SSN", "DL", "PASSPORT"). The AI must map each code to the correct Senzing feature. If your data has many identifier types, ask the AI to enumerate all possible values.
{{% /notice %}}

When you understand the strategy and have answered any questions:

**Tell Amazon Q:** `OK to proceed`
