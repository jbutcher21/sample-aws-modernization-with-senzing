---
title: "Running the Workshop in your own AWS Account"
chapter: true
weight: 22
draft: true
---

# Running the Workshop in your own AWS Account

{{% notice info %}}
Only follow the instructions in this section if you are using **your own account**. [Click here]({{< ref "/2_Setup_Configuration/21_AWS_Guided_Event" >}}) for instructions on running the workshop in an AWS-hosted event.
{{% /notice %}}

If you are running this workshop on your own AWS account, you will:

| Step | Action | Explanation |
|------|--------|-------------|
| 1 | [Configure IDE]({{< ref "/2_Setup_Configuration/_22_Own_AWS_Account/221_ConfigureIDE" >}}) | Setup Visual Studio Code with all needed plugins, dependencies, and download the workshop code. |
| 2 | [Setup Amazon Q Developer]({{< ref "/2_Setup_Configuration/23_AmazonQSetup" >}}) | Set up authentication for Amazon Q Developer in your IDE and the CLI using either your organization's IDC Professional license or using an AWS Builder ID. |

{{% notice warning %}}
If you are running this workshop on your own AWS account, remember to delete all resources by following the [Clean Up Resources]({{< ref "/7_Cleanup" >}}) section to avoid unnecessary charges.
{{% /notice %}}