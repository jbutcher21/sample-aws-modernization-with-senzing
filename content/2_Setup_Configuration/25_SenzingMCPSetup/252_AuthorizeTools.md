---
title: "Step 2: Authorize MCP Tools"
weight: 252
---

## Overview

After saving your MCP server configuration, Amazon Q will automatically detect the Senzing MCP tools and prompt you to authorize them.

## Authorization Prompt

You'll see a prompt showing all available Senzing tools:

![MCP Tools Authorization](/images/senzing_mcp/senzing_mcp5.png)

## Choose Authorization Level

{{% notice info %}}
**Choose your authorization preference:**
- **Always allow**: Recommended for workshop - allows Q to use these tools automatically
- **Ask**: You'll be prompted before each tool use (more manual but gives you control)
- **Deny**: Blocks the tool from being used
{{% /notice %}}

### Recommendation

**Select "Always allow"** for a smoother workshop experience.

This setting:
- Enables Amazon Q to automatically use Senzing tools when needed
- Eliminates repetitive authorization prompts
- Creates a more natural conversational AI experience
- Can be changed later in Amazon Q settings if needed

{{% notice tip %}}
"Always allow" is safe in this workshop environment since you control all the data and queries. In production environments with sensitive data, you might prefer "Ask" for additional oversight.
{{% /notice %}}

## Authorization Scope

The authorization applies to:
- All tools provided by the Senzing MCP server
- Future tool additions (if the MCP server is updated)
- Only this MCP server (doesn't affect other integrations)

## Next Steps

Once you've authorized the tools, you're ready to verify the integration is working correctly!

{{% notice info "Checkpoint" %}}
Ensure you've authorized at least some Senzing tools before proceeding to verification.
{{% /notice %}}
