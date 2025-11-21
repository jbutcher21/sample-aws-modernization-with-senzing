+++
title = "Senzing MCP Server Setup"
chapter = true
weight = 25
+++

## Overview

The Senzing MCP (Model Context Protocol) Server provides Amazon Q Developer with direct access to Senzing entity resolution capabilities. This integration allows you to interact with your Senzing database using natural language queries through Amazon Q.

In this section, you will:

1. Configure the pre-installed Senzing MCP server in Amazon Q Developer
2. Authorize MCP tools for Amazon Q to use
3. Verify the integration is working

{{% notice info %}}The MCP server provides 8+ tools for entity search, relationship analysis, and resolution explanation. This makes it easy to explore and understand entity resolution results using conversational AI.{{% /notice %}}

## Prerequisites

- Amazon Q Developer authenticated (configured in [previous section](../23_amazonqsetup))
- Senzing SDK installed and initialized in your environment (pre-configured in workshop)
- Senzing MCP server add on pre-installed (pre-configured in workshop)

## What You'll Learn

By the end of this section, you'll have:

- Connected Amazon Q Developer to the Senzing MCP server
- Authorized Senzing tools for use in your AI chat interface
- Verified the integration works with test queries
- Gained the ability to query entity resolution results conversationally

## Benefits of MCP Integration

Throughout this workshop, you'll use this integration to:

- Query entity resolution results conversationally
- Understand how Senzing identified duplicate entities
- Analyze relationships between resolved entities
- Get explanations of resolution decisions
- Explore your mapped data interactively

## Getting Started

Let's begin by configuring the MCP server connection!

{{% notice info %}}The setup process takes approximately 5-10 minutes. Follow each step carefully for a smooth experience.{{% /notice %}}
