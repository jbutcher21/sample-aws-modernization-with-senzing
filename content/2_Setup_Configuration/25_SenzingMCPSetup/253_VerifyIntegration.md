---
title: "Step 3: Verify the Integration"
weight: 253
---

## Overview

Now that you've configured and authorized the Senzing MCP server, let's verify that Amazon Q can successfully access and use the Senzing tools.

## Test 1: List Available Tools

1. **In the Amazon Q chat**, ask:

   ```
   What MCP tools are available?
   ```

![MCP Tools List](/static/images/senzing_mcp/senzing_mcp6.png)

::alert[These tools will become more useful once you've loaded entity data in later modules. For now, we're just confirming the connection works.]{type="info"}

## Test 2: Query Test Entity

2. **Try a test query:**

   ```
   Get entity1
   ```

![Test Entity Query](/static/images/senzing_mcp/senzing_mcp7.png)

### Expected Result

You should see a response indicating that entity 1 does not exist. This is expected because you haven't loaded any data yet.

The important part is that:
- Amazon Q successfully called the Senzing MCP tool
- The tool executed without errors
- You received a valid response (even though the entity doesn't exist)

::alert[A response like "entity 1 does not exist" or "no entity found" confirms the MCP server is working correctly!]{type="info"}

## What This Means

A successful response (even if the entity doesn't exist) indicates:

- ✅ Amazon Q is connected to the Senzing MCP server
- ✅ The MCP server can communicate with Senzing
- ✅ Environment variables are configured correctly
- ✅ Tools are authorized and functional

## Troubleshooting

If you encounter errors:

| Error | Possible Cause | Solution |
|-------|---------------|----------|
| "MCP server not found" | Configuration not saved | Revisit [Step 1](../251_configuremcpserver) |
| "Tool not authorized" | Authorization declined | Revisit [Step 2](../252_authorizetools) |
| "Connection timeout" | Senzing not installed | Contact workshop facilitator |
| "Database error" | Environment variables incorrect | Verify configuration in Step 1 |

## Wrap Up


Ensure the MCP server is configured and you can see Senzing tools in Amazon Q before proceeding.


Congratulations! You've successfully connected Amazon Q Developer to the Senzing MCP server!

### What You Can Do Now

Throughout this workshop, you'll use this integration to:

- Query entity resolution results conversationally
- Understand how Senzing identified duplicate entities
- Analyze relationships between resolved entities
- Get explanations of resolution decisions
- Explore your mapped data interactively

## Additional Resources

For more details on the Senzing MCP server:
- Review `/home/ubuntu/senzing-mcp-server/AMAZON_Q_SETUP.md` in your environment
- GitHub repository: [https://github.com/jbutcher21/senzing-mcp-server](https://github.com/jbutcher21/senzing-mcp-server)
- Amazon Q MCP Documentation: [https://docs.aws.amazon.com/amazonq/latest/qdeveloper-ug/mcp-ide.html](https://docs.aws.amazon.com/amazonq/latest/qdeveloper-ug/mcp-ide.html)
