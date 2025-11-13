---
title: "Step 4: Validate Mapping"
weight: 44
---

## Run the Mapper on Full Dataset

Now that you have a mapper, test it on the complete customer dataset to generate the Senzing JSON output.

### Execute the Mapper

**Tell Amazon Q:** `Run the mapper on the actual data`

![Output code and documentation 1](/images/exercise1/12-execute1.png)
![Output code and documentation 2](/images/exercise1/12-execute2.png)

Q will execute the mapper, run the linter, and run the JSON analyzer - all steps documented in the Senzing tools reference.

### Managing AI Context

If the analyzer output doesn't show errors or warnings, the AI may have lost context during the long conversation. When this happens, re-add the context using the `@` symbol.

{{% notice tip %}}
**Context Management:** Long conversations can cause AI to forget earlier instructions. Use the `@` symbol to re-add important reference files when needed.
{{% /notice %}}

**Re-add context to Amazon Q:**

1. In the Q chat input field, type `@` to open the context menu
2. Select `SENZING_TOOLS_REFERENCE.md` from the list
3. Press Enter to add it as context

**Tell Amazon Q:** `@SENZING_TOOLS_REFERENCE.md Rerun the json analyzer on the mapped customer JSON`

![Output code and documentation 1](/images/exercise1/12-execute3.png)
![Output code and documentation 2](/images/exercise1/12-execute4.png)
![Output code and documentation 2](/images/exercise1/12-execute5.png)

{{% notice info %}}
**About Warnings:** Warnings highlight data quality considerations, but they're informational. The data is what it is - it's just good to know these patterns in case something can be improved at the source!
{{% /notice %}}

{{% notice info %}}
**Checkpoint:** Your mapped data should pass validation with no errors. All 120 records should be valid Senzing JSON with features correctly recognized.
{{% /notice %}}
