---
title: "Configure your IDE"
weight: 221
---

## Prerequisites

For this workshop, you'll need:

| Tool | Purpose |
|------|---------|
| [Visual Studio Code](https://code.visualstudio.com/) | Integrated development environment (IDE) for writing, editing, and debugging code |
| [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html) | Command-line interface for AWS services, needed to interact with AWS resources and deploy the application |
| [Amazon Q CLI](https://docs.aws.amazon.com/amazonq/latest/qdeveloper-ug/command-line.html) | Command-line interface for Amazon Q Developer, enabling AI assistance directly from the terminal |
| [Amazon Q extension for Visual Studio Code](https://docs.aws.amazon.com/amazonq/latest/qdeveloper-ug/q-in-IDE-setup.html) | IDE extension that provides AI-powered code suggestions, chat assistance, and security scanning |
| [Git](https://github.com/git-guides/install-git/) | Version control system for managing workshop code and tracking changes |
| [Java - Amazon Corretto](https://aws.amazon.com/corretto) | Java runtime (version 17 or greater) needed to compile and run the Qordle application |
| [Maven](https://maven.apache.org/install.html) | Build automation tool for managing Java dependencies and building the application |

## Setup Instructions

1. Download the workshop code zip file:

   - [Java version](https://static.us-east-1.prod.workshops.aws/public/7cb92622-50d6-4bea-a78f-0b0af746aa23/assets/workshop.zip) - Contains Java code only
   - [All languages version](https://static.us-east-1.prod.workshops.aws/public/7cb92622-50d6-4bea-a78f-0b0af746aa23/assets/workshop-all.zip) - Contains Java, Python, C#, TypeScript and Node.js code

   {{% notice info %}}
   If you plan to use Python, C#, TypeScript or Node.js, download the All Languages version and refer to the [Additional Languages]({{< ref "/2_Setup_Configuration/24_AdditionalLanguages" >}}) guide.
   {{% /notice %}}

2. Unzip the file and open the `qwords-java` folder in VS Code (**File** → **Open Folder**).

3. Install the Amazon Q extension:

   - You many follow instructions at: [Installing the Q Developer Extension ...](https://docs.aws.amazon.com/amazonq/latest/qdeveloper-ug/q-in-IDE-setup.html#setup-vscode) or
   - Click the Extensions icon in the left sidebar
   - Search for "**Amazon Q**" and click Install

   ![Install Amazon Q extension](/images/on_your_own/q_plugin.png?height=150px)

4. Verify Java installation:

   {{< tabs >}}
   {{% tab name="MacOS" %}}
   ```bash
   /usr/libexec/java_home -V
   ```
   {{% /tab %}}

   {{% tab name="Windows" %}}
   ```bash
   java -version
   ```
   {{% /tab %}}

   {{% tab name="Linux" %}}
   ```bash
   java -version
   ```
   {{% /tab %}}
   {{< /tabs >}}

## Next Steps

You've successfully configured your IDE with all prerequisites. Proceed to [Connect using AWS Builder ID]({{< ref "/2_Setup_Configuration/23_AmazonQSetup" >}}) to connect to Amazon Q.