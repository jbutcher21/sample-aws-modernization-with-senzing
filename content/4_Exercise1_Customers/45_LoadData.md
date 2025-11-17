---
title: "Step 5: Load Data"
weight: 45
---

## Configure and Load Data into Senzing

Now that your mapping is validated, configure the DATA_SOURCE and load the customer data into Senzing for entity resolution.

### Step 1: Add the DATA_SOURCE

**Ask Amazon Q:** `Add the data source for me`

![Add data source 1](/images/exercise1/13-config1.png)
![Add data source 2](/images/exercise1/13-config2.png)

### Step 2: Load the Mapped Records

**Ask Amazon Q:** `Yes` to the prior question, or `load the mapped customer records into Senzing`

![Load Senzing 1](/images/exercise1/14-load1.png)
![Load Senzing 2](/images/exercise1/14-load2.png)


{{% notice info %}}
**Real-Time Resolution:** Unlike batch systems, Senzing resolves entities as data loads. By the time loading completes, all 120 records have been fully processed and resolved.
{{% /notice %}}

{{% notice info %}}
**Checkpoint:** All 120 customer records should be loaded with 8 redo records processed. No errors should occur.
{{% /notice %}}
