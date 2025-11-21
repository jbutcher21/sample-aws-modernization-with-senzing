+++
title = "Exercise 2: Watchlist"
chapter = true
weight = 6
+++

# Exercise 2: Watchlist

## Map and Load Watchlist Data

## Overview

In this exercise, you'll map watchlist data from JSON format (FollowTheMoney schema) to Senzing's entity resolution format. **Unlike Exercise 1, this is a self-guided workflow** - you'll take charge of the mapping process, questioning AI assumptions and making critical decisions.

Watchlist data is more complex than customer data, featuring:
- International names (Cyrillic, Arabic, Latin)
- Nested JSON structures with multiple schema types
- Entity relationships (ownership, directorships)
- Sanctions and compliance metadata

## What You'll Learn

By completing this exercise, you will:

- **Take charge of AI-assisted mapping** - Direct the workflow, question assumptions, verify decisions
- **Handle complex data structures** - Multi-pass processing for nested JSON with dependencies
- **Map international data** - Work with multiple character sets and transliterations
- **Process entity relationships** - Create networks using REL_POINTER patterns
- **Manage AI context** - Recover from context loss and session interruptions
- **Analyze cross-dataset resolution** - Discover hidden connections between customers and watchlist entities

## Exercise Format

This exercise uses a **self-guided workflow with key outcomes**:

1. **Before You Start** - Critical concepts and preparation
2. **Workflow Steps & Key Outcomes** - Complete 7-step mapping process with visual checkpoints
3. **Key Takeaways** - What you learned and how to apply it to your own data

**Estimated Time:** 45-60 minutes

::alert[**Important:** This exercise requires active participation. You'll need to question AI decisions, verify against actual data, and direct the workflow. Simply following prompts won't work - you must engage critically.]{type="warning"}

::alert[This exercise builds on Exercise 1. You'll see how watchlist entities resolve against customer data, revealing hidden networks and compliance risks.]{type="info"}

Let's get started!
