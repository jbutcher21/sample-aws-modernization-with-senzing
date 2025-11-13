---
title: "Step 6: Analyze Resolved Data"
weight: 46
---

## Capture and Analyze Entity Resolution Results

After loading data, take a snapshot and analyze how Senzing resolved your customer records. You'll explore statistics, understand match patterns, and investigate specific entity examples.

---

## Part 1: Take Snapshot

### Generate the Snapshot

**Ask Amazon Q:** `Yes` to the prior question, or `take a snapshot`

![Snapshot output 1](/images/exercise3/15-snapshot1.png)
![Snapshot output 2](/images/exercise3/15-snapshot2.png)

### Understanding the Results

**Key Result:** **120 records → 78 entities**

This means Senzing identified **42 duplicate records** (35% compression), consolidating them into their true entities.

### AI Analysis - Without You Even Asking

Look at what Amazon Q has already told you, without you even asking:

- Most of your matches were made on **name, address, and date of birth**
- There are **31 simple duplications** and **4 multi-record entities**
- The **compression rate was high** - did you expect that?
- An interesting entity to check out is **Entity 1, which has 5 records**

{{% notice tip %}}
**The Power of Proactive AI:** The AI didn't wait for you to ask questions - it analyzed the snapshot and surfaced the most important insights automatically. This is AI working for you.
{{% /notice %}}


### Traditional Analysis with sz_explorer

Traditionally, you would use Senzing's `sz_explorer` utility to review snapshots. You can still do this here!

**Ask Amazon Q:** `give me the command to open the snapshot with sz_explorer in a terminal using full paths to both`

**Open a new terminal:**

1. In your IDE, open the terminal (View → Terminal, or press Ctrl+`)
2. Paste and run the command Q provides

![EDA Tools](/images/exercise3/16-eda1.png)

This is the traditional exploratory data analysis (EDA) interface. It provides a command-line menu system to explore entities, relationships, and statistics.

{{% notice note %}}
**Traditional Workflow:** The `sz_explorer` tool is documented in the [Senzing EDA guide](https://senzing.zendesk.com/hc/en-us/articles/360051874294-Exploratory-Data-Analysis-3-Taking-a-snapshot). While powerful, it requires learning menu navigation and command syntax.
{{% /notice %}}

### Introducing Senzing's MCP Server!

Here's where it gets really cool. A snapshot only contains stats and entity IDs - no PII. That's where the MCP server comes in. Let's try a couple of things.

We already know that Entity 1 is the most interesting entity in the snapshot. So let's start there.

**Ask Amazon Q:** `who is entity 1`

![Get entity 1](/images/exercise3/17-entity1a.png)
![Get entity 2](/images/exercise3/17-entity1b.png)

Just like that, Q queries the Senzing MCP server and shows you the complete entity profile - all the records that merged, the features that matched, even the payload data. No command syntax. No menu navigation. Just ask.

### Need Technical Proof?

**Ask Amazon Q:** `how did senzing resolve entity 1`

![How entity 1](/images/exercise3/18-how1a.png)
![How entity 2](/images/exercise3/18-how1b.png)

Now you see the step-by-step resolution logic - which records merged when, what features matched at each step, even the similarity scores. This is the kind of detail that used to require digging through logs or complex API calls.

### The Questions Are Only Limited By Your Imagination

Try some of these:

**Ask Amazon Q:** `what possible matches should I review and why?`

**Ask Amazon Q:** `show me that drivers license and dob match`

**Ask Amazon Q:** `what relationships might qualify for a household and why? Can't just be same address, can it?`

{{% notice tip %}}
**Natural Language Exploration:** That last question about households? I had to refine it a bit to get exactly what I wanted. That's the beauty of conversational AI - you can iterate on your questions until you get the insight you're looking for. Try it yourself!
{{% /notice %}}

---

## Exercise 3 Complete!

{{% notice info %}}
**Checkpoint:** You've captured snapshots, analyzed resolution statistics, explored the traditional sz_explorer tool, and used the MCP server to conversationally investigate entity resolution decisions.
{{% /notice %}}

You now have hands-on experience with the complete Senzing workflow - from mapping to loading to analysis. More importantly, you've seen how AI assistance transforms every step: from generating schemas, to validating mappings, to exploring resolved entities.

**This is entity resolution, modernized.**
