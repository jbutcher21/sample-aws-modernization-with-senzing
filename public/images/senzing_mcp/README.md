# Senzing MCP Setup Screenshots

This directory contains screenshots for the Senzing MCP Server Setup section (25_SenzingMCPSetup.md).

## Required Screenshots

### 1. terminal_env_vars.png (height: 200px)
**Location in doc:** Step 1 - Verify Environment Variables
**Content:** Terminal window showing the output of:
```bash
echo $SENZING_ENGINE_CONFIGURATION_JSON
echo $LD_LIBRARY_PATH
echo $PYTHONPATH
```
**Notes:** Should show the actual environment variable values in the workshop environment

### 2. q_tools_icon.png (height: 150px)
**Location in doc:** Step 1 - Configure the MCP Server, Step 2
**Content:** Amazon Q chat interface highlighting the tools/wrench icon in the chat toolbar
**Notes:**
- Shows the tools icon location with arrow pointing to it
- Arrow should be blue (AWS blue: #0073BB) to match workshop style, not red
- This is the icon users click to access MCP server configuration
- Currently using AWS official tools icon from their docs as fallback

### 3. add_server.png (height: 200px)
**Location in doc:** Step 2 - Configure in Amazon Q Developer
**Content:** The "Add Server" dialog with STDIO transport type selection
**Notes:** Should show the transport type options clearly

### 4. mcp_config_form.png (height: 300px)
**Location in doc:** Step 2 - Configure in Amazon Q Developer
**Content:** MCP server configuration form with:
- Server Name: "Senzing MCP"
- Command: "/home/ubuntu/senzingMCP/launch_senzing_mcp.sh"
- Timeout: 60000
**Notes:** Show the form before environment variables are added

### 5. env_variables.png (height: 250px)
**Location in doc:** Step 2 - Configure in Amazon Q Developer
**Content:** The environment variables section showing all three variables being configured:
- SENZING_ENGINE_CONFIGURATION_JSON
- LD_LIBRARY_PATH
- PYTHONPATH
**Notes:** Should show the "Add Environment Variable" interface with at least one variable filled in

### 6. tool_authorization.png (height: 250px)
**Location in doc:** Step 3 - Authorize MCP Tools
**Content:** Amazon Q's tool authorization prompt showing the list of ~8 Senzing MCP tools
**Notes:** Should show the Auto-allow vs Ask each time options

### 7. verification_query.png (height: 200px)
**Location in doc:** Step 4 - Verify the Integration
**Content:** Amazon Q chat showing a successful query like "What MCP tools are available?" with Senzing tools listed in the response
**Notes:** Should demonstrate that the integration is working correctly

## Screenshot Guidelines

- Use consistent window sizing and theme throughout
- Ensure text is readable at the specified heights
- Capture at high resolution (2x or retina if possible)
- Use PNG format for crisp text rendering
- Highlight or annotate key areas if helpful (arrows, boxes, etc.)
- Match the visual style of other workshop screenshots (setup/, codeserver/, etc.)
