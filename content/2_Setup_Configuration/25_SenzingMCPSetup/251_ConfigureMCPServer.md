+++
title = "Step 1: Configure the MCP Server"
weight = 251
+++

## Overview

The Senzing MCP server and all required environment variables are pre-configured in your workshop environment. You just need to connect it to Amazon Q Developer.

## Access MCP Configuration

1. **Open the Amazon Q chat** panel in your IDE

2. **Click the tools icon** in the chat interface to access MCP configuration

![MCP Tools Icon](/images/senzing_mcp/senzing_mcp1.png)

3. **Select the plus (+) symbol** to add a new MCP server

![MCP Add Icon](/images/senzing_mcp/senzing_mcp2.png)

![MCP Tools Senzing Config](/images/senzing_mcp/senzing_mcp3.png)

## Choose Configuration Scope

4. **Choose your configuration scope:**
   - **Global** (recommended): Saves to `~/.aws/amazonq/default.json` - available for all projects
   - **Local**: Saves to `.amazonq/default.json` in current workspace only

{{% notice warning %}}We recommend **Global** scope so the Senzing MCP server is available in all your projects.]{type="info"}

## Configure Server Settings

5. **Fill in the MCP server configuration:**

   | Field | Value |
   |-------|-------|
   | **Server Name** | `Senzing` |
   | **Transport** | `stdio` |
   | **Command** | `/home/ubuntu/senzing-mcp-server/launch_senzing_mcp.sh` |
   | **Arguments** | (leave empty) |
   | **Timeout** | `60000` (60 seconds) |

   {{% notice info %}}Use the **full absolute path** for Command as shown above. This is the pre-installed location in your workshop environment.{{% /notice %}}

## Add Environment Variables

6. **Add Environment Variables:**

   Click "Add Environment Variable" three times and enter these exact values:

   | Variable Name | Value |
   |---------------|-------|
   | `SENZING_ENGINE_CONFIGURATION_JSON` | `{"PIPELINE":{"CONFIGPATH":"/etc/opt/senzing","RESOURCEPATH":"/opt/senzing/er/resources","SUPPORTPATH":"/opt/senzing/data"},"SQL":{"CONNECTION":"sqlite3://na:na@/home/ubuntu/sz_sqlite/G2C.db"}}` |
   | `LD_LIBRARY_PATH` | `/opt/senzing/er/lib` |
   | `PYTHONPATH` | `/home/ubuntu/.local/bin:/opt/senzing/er/sdk/python` |

   ::alert[Copy and paste each value exactly as shown. The `SENZING_ENGINE_CONFIGURATION_JSON` value should be on a single line.{{% /notice %}}

## Save Configuration

7. **Save the configuration**

Press the **Save** button to store your MCP server settings.

If you don't see the save button, you may see an error instead.

![MCP Configuration Error](/images/senzing_mcp/senzing_mcp4-error.png)

Make sure you're adding each environment variable as a **separate** key-value pair. Each variable name and its value should be entered individually, not combined as JSON.

## Troubleshooting

If you encounter issues:

- **Command path error**: Verify the path `/home/ubuntu/senzing-mcp-server/launch_senzing_mcp.sh` exists
- **Environment variables error**: Ensure each variable is entered separately, not as a JSON object
- **Timeout issues**: The 60-second timeout should be sufficient; if not, check Senzing installation

Once you see a successful save (no error message), proceed to authorize the MCP tools.

