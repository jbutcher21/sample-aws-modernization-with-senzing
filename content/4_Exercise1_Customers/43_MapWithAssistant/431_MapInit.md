+++
title = "Stage 1: INIT"
weight = 431
+++

## Stage 1: INIT - Load References

Start the Mapping Assistant to load the Senzing specification and examples into Q's context.

### Launch the Mapping Assistant

Open Amazon Q Developer (if not already open)

**Tell Amazon Q:** `Start the senzing mapping assistant`

![Mapping Assistant 1](/images/exercise1/6-assistant1.png)
![Mapping Assistant 2](/images/exercise1/6-assistant2.png)

### Why This Matters

By loading these references, the AI can:
- Make informed mapping decisions based on the official specification
- Cite specific sections when explaining choices
- Validate mappings against real examples
- Prevent hallucination by working from authoritative sources

The assistant will now confirm: **"✅ STAGE 1 COMPLETE - Ready for INVENTORY"**

{{% notice info %}}**Interactive Learning:** If you're curious about any reference file, you can ask Q to explain it. For example: "What's in the identifier crosswalk?"{{% /notice %}}

{{% notice info %}}**Checkpoint:** Q should confirm all 5 reference files are loaded and the linter tool is validated.{{% /notice %}}
