# 1. Create a semantic model in Fabric

Use the included workbook to create a schema-enabled lakehouse and a validated Direct Lake semantic model.

## Sign in

Open a terminal in the repository root and sign in:

```text
az login --tenant <TENANT_ID>
```

## Pick your prompt

Choose **one** option, replace the placeholders, and paste it into your coding agent:

| Option | Approach |
|---|---|
| [Detailed instructions](#option-1-detailed-instructions) | Specify the tables, relationships, measures, and roles for a consistent lab result. |
| [Let the agent decide](#option-2-let-the-agent-decide) | Describe the goal and let the agent choose the model design from the workbook. Results may differ. |

Both options load the workbook into a schema-enabled lakehouse, use your alias, and deploy and validate a Direct Lake model. Do not run both.

## Option 1: Detailed instructions

```text
Create the Fabric data foundation for a Northwind procurement spend app.
Use the installed Fabric skills for ingestion and semantic-model-authoring
for the model.

Inputs:
- Workbook: data/Northwind_Spend_Extract_FY2026.xlsx
- Alias: <ALIAS>
- Tenant ID: <TENANT_ID>
- Fabric workspace name: <WORKSPACE_NAME>

Ask for any missing inputs. Use my alias in every Fabric item name.
Check for existing items before creating them, and do not overwrite
another participant's work.

Read the workbook's README and load its five data sheets into the
schema-enabled lakehouse northwind_lh_<ALIAS>. Upload the workbook to
Files/raw/ and create and run load_spend_workbook_<ALIAS> to load:
- Spend_Lines -> dbo.spend_lines
- Suppliers -> dbo.suppliers
- Categories -> dbo.categories
- Business_Units -> dbo.business_units
- Calendar -> dbo.calendar
Make reruns safe for these lab tables. Keep IDs and po_number as text
and dates as date values. Identify suppliers by supplier_id, not name,
and retain Unmapped categories. Validate counts, types, and spend through
the SQL endpoint; refresh its metadata and retry if tables are not visible.

Author Northwind Spend Model - <ALIAS> as a complete TMDL model, then
deploy it using Direct Lake over all five tables with schemaName: dbo.
Add many-to-one, single-direction relationships from spend_lines:
- supplier_id -> suppliers[supplier_id]
- category_l2 -> categories[category_l2]
- business_unit -> business_units[business_unit]
- invoice_date -> calendar[date]
Mark calendar as the date table, sort month_name by month_number,
and hide spend_lines[supplier_id], po_number, and invoice_line_id.

Add these 15 measures to spend_lines, each with a description:
- Total Spend: sum of invoice_amount_usd.
- Addressable Spend: spend in addressable categories.
- Addressable %: Addressable Spend / Total Spend.
- Savings Opportunity Low: sum of category spend times its low savings rate.
- Savings Opportunity Mid: average of the low and high opportunities.
- Savings Opportunity High: sum of category spend times its high savings rate.
- Supplier Count: distinct suppliers with spend.
- Invoice Lines: count of invoice lines.
- Non-PO Spend %: spend share where po_flag = Non-PO.
- Tail Spend %: spend share with Tail-tier suppliers.
- Contract Coverage %: spend share with suppliers under contract.
- Unmapped Spend %: spend share in the Unmapped category.
- Top 10 Supplier Share %: spend share with the ten largest suppliers.
- Weighted Payment Terms (days): payment terms weighted by invoice amount.
- Spend % of Revenue: spend divided by business-unit revenue.
Format monetary measures as $#,0.0,,"M", percentages as 0.0%,
counts as #,0, and payment terms as 0.0.
Use each category's own savings rate and the workbook's percentage units.
Convert business-unit revenue from millions to dollars before dividing.

Add three RLS roles with read permission:
- Aerospace only: business_units[business_unit] = "Aerospace Components".
- BU lead (dynamic): business_units[bu_lead_email] = USERPRINCIPALNAME().
- Engagement team: no filter.

Validate all 15 measures with DAX through the executeQueries API against
independent workbook calculations, including business-unit/category slices.
Check role definitions; mark runtime RLS unverified if no Viewer test
identity is available, since Admin/Member accounts bypass RLS.

Report the workspace, lakehouse, notebook, and semantic model IDs,
validation results, and anything that could not be verified.
Stop after the semantic model is ready; do not build the app yet.
```

## Option 2: Let the agent decide

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

For the detailed option, expect **five tables, four relationships, 15 measures, and three roles**. For the flexible option, review the agent's chosen design and how it supports the requested analysis.

[Next: Build a visualization](../02-build-visualization/README.md)

[Back to the hackathon](../../../README.md#lets-get-started)
