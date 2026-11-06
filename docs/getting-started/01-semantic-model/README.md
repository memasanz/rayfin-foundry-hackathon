# 1. Create a semantic model in Fabric

Use the included workbook to create a schema-enabled lakehouse and a validated Direct Lake semantic model.

## Sign in

Open a terminal in the repository root and sign in:

```text
az login --tenant <TENANT_ID>
```

## Prompt

Replace the placeholders and paste this into your coding agent:

```text
Explore the Northwind spend workbook included in this repository, load it
into a schema-enabled Fabric lakehouse with tables in the dbo schema,
and create a Direct Lake semantic model for a procurement spend app.

Inputs:
- Workbook: data/Northwind_Spend_Extract_FY2026.xlsx
- Alias: <ALIAS>
- Tenant ID: <TENANT_ID>
- Fabric workspace name: <WORKSPACE_NAME>

Use my alias in every Fabric item name so my work stays separate from
other participants:
- Lakehouse: northwind_lh_<ALIAS>
- Loading notebook: load_spend_workbook_<ALIAS>
- Semantic model: Northwind Spend Model - <ALIAS>
Ask for any missing inputs and check for existing items before creating
them. Do not overwrite another participant's work.

Read the workbook's README and explore its sheets. Use the installed Fabric
and semantic-model-authoring skills to handle ingestion and model design,
including appropriate data types, relationships, and business measures.
Choose the design based on the workbook rather than asking me to specify
every table and measure. Ensure the Direct Lake model uses the lakehouse's
dbo schema.
The model should support analysis of spend, suppliers, categories,
business units, trends, and potential savings.

Deploy the model and validate it against the workbook. Summarize the data,
your modeling choices, validation results, and the workspace and model IDs
we will need to build the app.

Stop after the semantic model is ready; do not build the app yet.
```

## Check the result

Review the agent's summary and confirm that the model is deployed and its results reconcile to the workbook. Keep the reported workspace and model IDs for the next task.

[Next: Build a visualization](../02-build-visualization/README.md)

[Back to the hackathon](../../../README.md#lets-get-started)
