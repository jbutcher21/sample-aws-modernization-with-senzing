+++
title = "Amazon Q Setup"
weight = 23
+++

## Overview

In this section, you will:

1. Set up authentication for **both** the Amazon Q IDE extension and CLI using AWS Builder ID

::alert[*Using [AWS IAM Identity Center](https://docs.aws.amazon.com/singlesignon/latest/userguide/what-is.html)?* See the [Amazon Q Developer documentation](https://docs.aws.amazon.com/amazonq/latest/qdeveloper-ug/getting-started-idc.html) for instructions on connecting Amazon Q with your IDC configuration.]{type="info"}

:::expand{header="Don't have an AWS Builder ID?"}

[AWS Builder ID](https://profile.aws.amazon.com/) is a personal profile that provides access to select tools and services including Amazon CodeCatalyst, Amazon Q Developer, and AWS Training and Certification. AWS Builder ID is free and you don't need to enter any credit card details upon creation of a profile. For more information, refer to the [documentation](https://docs.aws.amazon.com/signin/latest/userguide/differences-aws_builder_id.html).

To create a profile:

![AWS Builder ID Creation](/images/setup/builder-id.png?height=500px)

- Enter your email address → **Next**.
- Enter your name → **Next**.
- Check your email for a verification code (subject: "Verify your AWS Builder ID email address")
- Enter the verification code → **Verify**
- Create a password → **Create AWS Builder ID**

:::

2. Enable workspace indexing for enhanced AI assistance

## Authentication Setup

::alert[**Important:**.*]{type="warning"}

::::tabs{variant="container"}

:::tab{label="IDE Plugin"}

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

:::

:::tab{label="CLI"}

1. In your terminal, run:

   ```bash
   q login
   ```

2. Select **Use for Free with Builder ID** and press **Enter**

![Q CLI Login](/images/setup/q-cli-login.gif?height=250px)

3. Open the provided URL in your browser:

- Select **Confirm and continue**
- Select **Allow access**
- After seeing "Request approved", return to your terminal

4. Test your setup with:

   ```bash
   q chat "Hello, Amazon Q!" --no-interactive
   ```

![Q CLI Chat](/images/setup/q-cli-chat.gif?height=300px)

:::

::::

## Enable Additional Features

::::tabs{variant="container"}

:::tab{label="IDE Plugin"}

### Enable Workspace Context

To make Amazon Q aware of your entire codebase:

1. Click on 'Amazon Q' in the status bar
2. Select **'Open Settings'**
3. Select the check-box under **Amazon Q: Workspace Index** to enable workspace indexing

![Workspace Index](/images/setup/workspace-index.gif?height=500px)

::alert[Initial workspace indexing takes 1-20 minutes and may increase CPU usage. Subsequent changes update the index incrementally.]{type="info"}

#### Example queries using workspace context

- 💬 `@workspace` `Where is the business logic to handle users?`
- 💬 `@workspace` `Explain the data flow between the front-end and back-end.`
- 💬 `Add new API tests using the existing test utilities found in the @workspace.`

:::

:::tab{label="CLI"}

### Experimental Features

The CLI provides access to experimental features that you can optionally enable:

1. Launch the Q chat interface:

```bash
q chat
```

2. Access the experiments section:

```bash
/experiment
```

3. Browse and toggle available experimental features:

- Use Spacebar to enable/disable features

**Note: No experimental features are required for this workshop.**

![Q CLI Experiments](/images/setup/cli-experiments.png?height=200px)

:::

::::

## Wrap up

::alert[**Checkpoint:** Ensure you have completed authentication and feature setup for both the IDE Plugin and CLI before proceeding.]{type="info"}

You've now configured Amazon Q in both your IDE and CLI using your AWS Builder ID, giving you AI assistance across different interfaces.

