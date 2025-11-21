---
title: "Configure your IDE"
weight: 221
---

## Prerequisites

For this workshop, you'll need:

| Tool | Purpose |
|------|---------|
| [Visual Studio Code](https://code.visualstudio.com/) | Integrated development environment (IDE) for writing, editing, and debugging code |
| [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html) | Command-line interface for AWS services, needed to interact with AWS resources |
| [Amazon Q CLI](https://docs.aws.amazon.com/amazonq/latest/qdeveloper-ug/command-line.html) | Command-line interface for Amazon Q Developer, enabling AI assistance directly from the terminal |
| [Amazon Q extension for Visual Studio Code](https://docs.aws.amazon.com/amazonq/latest/qdeveloper-ug/q-in-IDE-setup.html) | IDE extension that provides AI-powered code suggestions, chat assistance, and security scanning |
| [Git](https://github.com/git-guides/install-git/) | Version control system for managing workshop code and tracking changes |

## Setup Instructions

1. Clone or download the workshop repository:

   ```bash {copy}
   git clone https://github.com/your-org/senzing-workshop.git
   cd senzing-workshop
   ```

2. Open the workshop folder in VS Code (**File** → **Open Folder**).

3. Install the Amazon Q extension:

   - You may follow instructions at: [Installing the Q Developer Extension](https://docs.aws.amazon.com/amazonq/latest/qdeveloper-ug/q-in-IDE-setup.html#setup-vscode) or
   - Click the Extensions icon in the left sidebar
   - Search for "**Amazon Q**" and click Install

   ![Install Amazon Q extension](/static/images/on_your_own/q_plugin.png)

## Next Steps

You've successfully configured your IDE with all prerequisites. Proceed to [Connect using AWS Builder ID](/2_Setup_Configuration/23_AmazonQSetup) to connect to Amazon Q.
