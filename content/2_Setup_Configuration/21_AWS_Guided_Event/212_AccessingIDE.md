---
title: "Accessing your IDE"
weight: 212
---

### Access your cloud-based code-server IDE

For this workshop, you'll use Visual Studio Code running on an Amazon EC2 instance via code-server. This provides a consistent development environment with all tools pre-configured.

1. Open the [Workshop Studio event dashboard](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US)

2. Navigate to the **Event Outputs** panel at the bottom of the page.

   ![Event Outputs](/images/codeserver/event_outputs.png?height=150px)

3. Copy the **Password** 🔑 - you'll need this to authenticate.

4. Click on the **URL** to open your cloud IDE in a new tab.

5. In the **Welcome to code-server** dialog, paste the password you copied and choose **Submit**.

   ![Submit](/images/codeserver/submit.png?height=180px)

   {{% notice info %}}
   **Tip:** If the login fails, verify you copied the complete password without extra spaces.
   {{% /notice %}}

6. You should now see the code-server IDE interface with the file explorer on the left.

   ![Code-server IDE](/images/codeserver/codeserver.png?height=300px)

## Pre-packaged components

Your cloud IDE comes with all necessary tools pre-installed:

| Tool | Purpose |
|------|---------|
| [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html) | Command-line interface for AWS services, needed to interact with AWS resources and deploy the application |
| [Amazon Q CLI](https://docs.aws.amazon.com/amazonq/latest/qdeveloper-ug/command-line.html) | Command-line interface for Amazon Q Developer, enabling AI assistance directly from the terminal |
| [Amazon Q extension for Visual Studio Code](https://docs.aws.amazon.com/amazonq/latest/qdeveloper-ug/q-in-IDE-setup.html) | IDE extension that provides AI-powered code suggestions, chat assistance, and security scanning |
| [Git](https://github.com/git-guides/install-git/) | Version control system for managing workshop code and tracking changes |
| [Java - Amazon Corretto](https://aws.amazon.com/corretto) | Java runtime (version 17 or higher) needed to compile and run the Qordle application |
| [Maven](https://maven.apache.org/install.html) | Build automation tool for managing Java dependencies and building the application |

📁 **Workshop Code Location:** The sample code repository has been downloaded into the `/Workshop/java` folder.

## Wrap up

You have successfully accessed your VS code-server IDE, which has been pre-configured for the workshop. Please move to the next section where you will authenticate with the Amazon Q Developer extension and CLI.

{{% notice info %}}
**Next Step:** Proceed to [Amazon Q Authentication Setup]({{< ref "/2_Setup_Configuration/23_AmazonQSetup" >}}) to connect to Amazon Q Developer.
{{% /notice %}}