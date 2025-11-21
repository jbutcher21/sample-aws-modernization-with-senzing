+++
title = "Accessing your IDE"
weight = 212
+++

### Access your cloud-based code-server IDE

For this workshop, you'll use Visual Studio Code running on an Amazon EC2 instance via code-server. This provides a consistent development environment with all tools pre-configured.

1. Open the [Workshop Studio event dashboard](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US)

2. Navigate to the **Event Outputs** panel at the bottom of the page.

   ![Event Outputs](/images/codeserver/event_outputs.png?height=150px)

3. Copy the **Password** 🔑 - you'll need this to authenticate.

4. Click on the **URL** to open your cloud IDE in a new tab.

5. In the **Welcome to code-server** dialog, paste the password you copied and choose **Submit**.

   ![Submit](/images/codeserver/submit.png?height=180px)

   {{% notice info %}}**Tip:** If the login fails, verify you copied the complete password without extra spaces.{{% /notice %}}

6. You should now see the code-server IDE interface with the file explorer on the left.

   ![Code-server IDE](/images/codeserver/codeserver.png?height=300px)

## Pre-packaged components

Your cloud IDE comes with all necessary tools pre-installed:

| Tool | Purpose |
|------|---------|
| [Senzing SDK](https://senzing.com/) (version 4.0) | Entity resolution engine - installed and configured with an empty database |
| [Amazon Q extension for Visual Studio Code](https://docs.aws.amazon.com/amazonq/latest/qdeveloper-ug/q-in-IDE-setup.html) | IDE extension that provides AI-powered code suggestions, chat assistance, and MCP server support |
| [senzing-mcp-server](https://github.com/jbutcher21/senzing-mcp-server) | Model Context Protocol server that connects Amazon Q to Senzing capabilities |

📁 **Workshop Materials Location:** Workshop files and Senzing resources are located in `/home/ubuntu/`

## Wrap up

You have successfully accessed your VS code-server IDE, which has been pre-configured for the workshop. Please move to the next section where you will authenticate with the Amazon Q Developer extension and CLI.

{{% notice info %}}**Next Step:** Proceed to [Amazon Q Authentication Setup](/2_Setup_Configuration/23_AmazonQSetup) to connect to Amazon Q Developer.{{% /notice %}}