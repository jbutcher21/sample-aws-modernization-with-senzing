---
title: "Exercise 2: Watchlist"
chapter: true
weight: 5
---

# Exercise 2: Watchlist

## Map and Load Watchlist Data

## Overview

In this exercise, you'll map watchlist data from JSON format (FollowTheMoney schema) to Senzing's entity resolution format. Watchlist data is more complex than customer data, featuring international names, relationships, and sanctions information.

## What You'll Learn

By completing this exercise, you will:

- Work with JSON source data (vs CSV from Exercise 1)
- Handle complex nested data structures
- Map international names and identifiers
- Process entity relationships
- Combine watchlist data with existing customer data
- Analyze cross-dataset entity resolution

## Exercise Steps

This exercise follows the same 8-step workflow as Exercise 1:

1. **Examine the source data** - Understand watchlist JSON structure
2. **Provide or create the schema** - Document the data structure
3. **Use the Senzing Mapping Assistant** - AI-guided mapping workflow
4. **Validate the mapping** - Verify output with JSON analyzer
5. **Load the data in Senzing** - Import mapped records
6. **Take a snapshot** - Capture resolution results
7. **Analyze the snapshot** - Review statistics and examples
8. **Review with MCP server** - Ask how and why questions

**Estimated Time:** 30-45 minutes

{{% notice tip %}}
Watchlist data presents new challenges: nested JSON structures, international names, and relationships. Apply what you learned in Exercise 1!
{{% /notice %}}

{{% notice info %}}
This exercise builds on Exercise 1. You'll see how watchlist entities resolve against customer data.
{{% /notice %}}

Let's get started!
