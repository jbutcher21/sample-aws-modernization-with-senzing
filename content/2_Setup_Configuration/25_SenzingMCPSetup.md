---
title: "Senzing MCP Server Setup"
weight: 25
---

## Overview

The Senzing MCP (Model Context Protocol) Server provides Amazon Q Developer with direct access to Senzing entity resolution capabilities. This integration allows you to interact with your Senzing database using natural language queries through Amazon Q.

In this section, you will:

1. Configure the pre-installed Senzing MCP server in Amazon Q Developer
2. Authorize MCP tools for Amazon Q to use
3. Verify the integration is working

{{% notice info %}}
The MCP server provides 8+ tools for entity search, relationship analysis, and resolution explanation. This makes it easy to explore and understand entity resolution results using conversational AI.
{{% /notice %}}

## Prerequisites

{{% notice info "Required" %}}
- Amazon Q Developer authenticated (configured in [previous section](../23_amazonqsetup))
- Senzing SDK installed and initialized in your environment (pre-configured in workshop)
- Senzing MCP server add on pre-installed (pre-configured in workshop)
{{% /notice %}}

## Step 1: Configure the MCP Server

The Senzing MCP server and all required environment variables are pre-configured in your workshop environment. You just need to connect it to Amazon Q Developer.

1. **Open the Amazon Q chat** panel in your IDE

2. **Click the tools icon** in the chat interface to access MCP configuration

![MCP Tools Icon](/images/senzing_mcp/senzing_mcp1.png)

3. **Select the plus (+) symbol** to add a new MCP server

![MCP Add Icon](/static/images/senzing_mcp/senzing_mcp2.png)

![MCP Tools Senzing Config](/static/images/senzing_mcp/senzing_mcp3.png)

4. **Choose your configuration scope:**
   - **Global** (recommended): Saves to `~/.aws/amazonq/default.json` - available for all projects
   - **Local**: Saves to `.amazonq/default.json` in current workspace only

5. **Fill in the MCP server configuration:**

   | Field | Value |
   |-------|-------|
   | **Server Name** | `Senzing` |
   | **Transport** | `stdio` |
   | **Command** | `/home/ubuntu/senzing-mcp-server/launch_senzing_mcp.sh` |
   | **Arguments** | (leave empty) |
   | **Timeout** | `60000` (60 seconds) |

   {{% notice warning %}}
   Use the **full absolute path** for Command as shown above. This is the pre-installed location in your workshop environment.
   {{% /notice %}}

6. **Add Environment Variables:**

   Click "Add Environment Variable" three times and enter these exact values:

   | Variable Name | Value |
   |---------------|-------|
   | `SENZING_ENGINE_CONFIGURATION_JSON` | `{"PIPELINE":{"CONFIGPATH":"/etc/opt/senzing","RESOURCEPATH":"/opt/senzing/er/resources","SUPPORTPATH":"/opt/senzing/data"},"SQL":{"CONNECTION":"sqlite3://na:na@/home/ubuntu/sz_sqlite/G2C.db"}}` |
   | `LD_LIBRARY_PATH` | `/opt/senzing/er/lib` |
   | `PYTHONPATH` | `/home/ubuntu/.local/bin:/opt/senzing/er/sdk/python` |

   {{% notice tip %}}
   Copy and paste each value exactly as shown. The `SENZING_ENGINE_CONFIGURATION_JSON` value should be on a single line.
   {{% /notice %}}

7. **Save the configuration**

Press the **Save** button to store your MCP server settings.

If you don't see the save button, you may see an error instead.

![MCP Tools Senzing Config](/static/images/senzing_mcp/senzing_mcp4-error.png)  


   {{% notice warning "Common Mistake" %}}
   Make sure you're adding each environment variable as a **separate** key-value pair. Each variable name and its value should be entered individually, not combined as JSON.
   {{% /notice %}}
   
## Step 2: Authorize MCP Tools

After saving, Amazon Q will automatically detect the Senzing MCP tools and prompt you to authorize them.

![MCP Tools Senzing Config](/static/images/senzing_mcp/senzing_mcp5.png)  

You'll see a list of approximately 8 tools, including:

{{% notice info %}}
**Choose your authorization preference:**
- **Always allow**: Recommended for workshop - allows Q to use these tools automatically
- **Ask**: You'll be prompted before each tool use (more manual but gives you control)
- **Deny**: Blocks the tool from being used
{{% /notice %}}

**Recommendation:** Select **Always allow** for a smoother workshop experience.

## Step 3: Verify the Integration

Test that Amazon Q can access the Senzing MCP server:

1. **In the Amazon Q chat**, ask:

   ```
   What MCP tools are available?
   ```
![MCP Tools Senzing Config](/static/images/senzing_mcp/senzing_mcp6.png)

These tools will be available for use in your Amazon Q chat interface once data has been loaded!

2. **Try a test query:**

   ```
   Get entity1
   ```
![MCP Tools Senzing Config](/static/images/senzing_mcp/senzing_mcp7.png)

Of course, entity 1 does not yet exist as we have not loaded data.  But a reponse like this indicates that the MCP server is working!

## Wrap up

{{% notice info "Checkpoint" %}}
Ensure the MCP server is configured and you can see Senzing tools in Amazon Q before proceeding.
{{% /notice %}}

You've successfully connected Amazon Q Developer to the Senzing MCP server! Throughout this workshop, you'll use this integration to:

- Query entity resolution results conversationally
- Understand how Senzing identified duplicate entities
- Analyze relationships between resolved entities
- Get explanations of resolution decisions
- Explore your mapped data interactively

You're now ready to learn about Senzing mapping concepts!

{{% notice info %}}
**Next Step:** Proceed to [Module 3: Understanding Senzing Mapping](../../3_understandingmapping)
{{% /notice %}}

## Additional Resources

For more details on the Senzing MCP server:
- Review `/home/ubuntu/senzing-mcp-server/AMAZON_Q_SETUP.md` in your environment
- GitHub repository: [https://github.com/jbutcher21/senzing-mcp-server](https://github.com/jbutcher21/senzing-mcp-server)
- Amazon Q MCP Documentation: [https://docs.aws.amazon.com/amazonq/latest/qdeveloper-ug/mcp-ide.html](https://docs.aws.amazon.com/amazonq/latest/qdeveloper-ug/mcp-ide.html)
