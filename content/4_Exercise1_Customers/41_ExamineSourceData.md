---
title: "Step 1: Examine Source Data"
weight: 41
---

## Understanding Your Source Data

Before mapping data to Senzing format, you need to understand what you're working with. In this step, you'll examine the customer CSV file to identify its structure, fields, and business purpose.

## Open the Customer Data File

**Navigate to the source data:**
1. In your IDE file explorer (left sidebar), expand the workshop folder
2. Navigate to `workshop/workspace/customers/`
3. Double-click `customers.csv` to open it in the editor

![Customer CSV file open in IDE](/images/exercise1/1-customer.png)

## Explore the Data Structure

Take a few minutes to review the CSV file. Ask yourself these questions:

**About the data structure:**
- What columns are present?
- What types of data do you see? (names, addresses, identifiers, dates, etc.)
- Are there any empty or inconsistent values?

**About the business purpose:**
- Why are you loading this data into Senzing?
  - Are you looking for duplicate customer records?
  - Will you compare this against a watchlist later?
  - Do you need to consolidate customer identities?

Understanding both the structure and purpose of your data will help you guide the AI to create an effective mapping.

{{% notice tip %}}
**Key Insight:** You don't need to memorize every field - just get familiar with what's there. The AI will help with the detailed mapping, but you need to provide the business context and mapping strategy.
{{% /notice %}}

{{% notice info %}}
**Checkpoint:** You should understand the basic structure of the customer data and why you're loading it into Senzing before proceeding to the next step.
{{% /notice %}}
