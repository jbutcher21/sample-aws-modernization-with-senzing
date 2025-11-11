---
title: "Amazon Q Setup"
weight: 23
---

## Overview

In this section, you will authenticate the Amazon Q IDE extension using AWS Builder ID.

{{% notice info %}}
This workshop uses AWS Builder ID for authentication. Builder ID is free and doesn't require an AWS account.
{{% /notice %}}

{{% expand "Don't have an AWS Builder ID?" %}}
[AWS Builder ID](https://profile.aws.amazon.com/) is a personal profile that provides access to select tools and services including Amazon CodeCatalyst, Amazon Q Developer, and AWS Training and Certification. AWS Builder ID is free and you don't need to enter any credit card details upon creation of a profile. For more information, refer to the [documentation](https://docs.aws.amazon.com/signin/latest/userguide/differences-aws_builder_id.html).

To create a profile:

![AWS Builder ID Creation](/images/setup/builder-id.png?height=300px)

- Enter your email address -> **Next**.
- Enter your name -> **Next**.
- Check your email for a verification code (subject: "Verify your AWS Builder ID email address")
- Enter the verification code -> **Verify**
- Create a password -> **Create AWS Builder ID**
{{% /expand %}}

## Authentication Setup

1. In the Amazon Q extension, select **Use for free** → **Continue**.

![Amazon Q extension set up](/images/codeserver/codeserver.png?height=300px)

2. When prompted, select **Proceed to Browser**

![Confirm Code](/images/builder_id/confirm_code.png?height=175px)

3. When asked "Do you want Code (or code-sever) to open the external website?", choose **Open**.

![Trust Domain](/images/builder_id/trust_domain.png?height=175px)

4. In the browser:

- You will be redirected to the AWS Builder ID Login flow. Login with your credentials.

- Confirm the pre-populated code by clicking **Confirm and continue**.

  ![Code Verification](/images/setup/code-verification.png?height=250px)

- Select **Allow access** when prompted

- You'll see a "**Request approved**" confirmation

- Return to your IDE

## Wrap up

{{% notice info %}}
**Checkpoint:** Verify that Amazon Q shows you're authenticated before proceeding.
{{% /notice %}}

You've successfully authenticated Amazon Q Developer in your IDE. You're now ready to configure the Senzing MCP Server!