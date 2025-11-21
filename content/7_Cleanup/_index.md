+++
title = "Clean Up Resources"
chapter = true
weight = 7
+++

## Overview

If you ran this workshop in your own AWS account, it's important to clean up the resources you created to avoid ongoing charges.

## Resources to Clean Up

Depending on which parts of the workshop you completed, you may have created the following resources:

- Amazon Q Developer configurations (no charges)
- Any AWS services used during the workshop exercises

## Cleanup Steps

### 1. Amazon Q Developer

Amazon Q Developer authentication and IDE configurations don't incur charges, but you can disconnect if desired:

- In VS Code, you can sign out of Amazon Q through the extension settings
- CLI authentication can be cleared with `q logout` (if available)

### 2. AWS Resources

If you created any AWS resources during the workshop:

1. **Review your AWS Console** for any resources created during the workshop
2. **Delete resources** in the reverse order of creation to avoid dependency issues
3. **Check for any CloudFormation stacks** that may have been created
4. **Verify S3 buckets** are empty before deletion

## Verification

To ensure all resources are cleaned up:

1. Check your AWS billing dashboard for any unexpected charges
2. Review the AWS Cost Explorer for resource usage during the workshop period
3. Set up billing alerts if you haven't already

{{% notice info %}}Most of this workshop focuses on Amazon Q Developer setup and configuration, which doesn't create billable AWS resources. However, always verify your account to ensure no unexpected resources remain.{{% /notice %}}

## Need Help?

If you're unsure about any resources or cleanup steps:

- Review the AWS documentation for the specific services you used
- Contact AWS Support if you have questions about billing or resource cleanup
- Check the AWS forums for community assistance