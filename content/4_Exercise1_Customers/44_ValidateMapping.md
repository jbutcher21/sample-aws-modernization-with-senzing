---
title: "Step 4: Validate Mapping"
weight: 44
---

Before you validate the entire mapping you have to run the mapper and the actual data

Tell amazonq: Go ahead and run the mapper and the actual data

image4-validate0.png on images/exercise1

Like the linting process, it may catch errors and correct them.  Usually it sees the problem and fixes it.  If it cannot fix it, it will report the error and you will have to go back and correct the mapping. 

These kinds of errors can also occur as we mapped from the schema, not the actual data.  This is where the rubber meets the road and you may learn even more about your data. So pay attention so you can maybe catch these things earlier in the process.

as before this is a great learning opportunity!

When it does fisnish you will see a report like this:

image4-validate0b.png on images/exercise1

## Validate the Mapping with JSON Analyzer

It also knows the next step is the json analyzer and may even run it for you.  If not you can run it yourself.

Tell amazonq: Run the JSON analyzer on the mapped customer JSON

Why run the json analyzer? Because it runs a different set of checks than the linting process which just says senzing can load it.  The json analyzer produces errors, warnings and information about your data. Such as low population percents, values that are expected to be more unique than they are.  


See what it says about your mapped customer data!

You will see the following:

image4-validate1.png on images/exercise1
image4-validate2.png on images/exercise1
image4-validate3.png on images/exercise1

Of course any errors need to be addressed, but as far as the warnings and info ... In the end, the data is what it is.  it just nice to know these things in case something can be done about it!

Double check to see if there were any errors

Ask amazonq: were there any errors

image4-validate3.png on images/exercise1

You can even ask the AI to add the data source for you!

tell amazonq: add the data source for me



{{% notice info %}}
**Checkpoint:** Your mapped data should pass validation with no errors.
{{% /notice %}}
