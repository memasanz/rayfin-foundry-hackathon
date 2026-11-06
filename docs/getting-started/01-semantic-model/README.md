# 1. Create a semantic model in Fabric

Use the included workbook to create a lakehouse and a validated Direct Lake semantic model.

## Sign in

Open a terminal in the repository root and sign in:

```text
az login --tenant <TENANT_ID>
```

## Prompt

Replace the placeholders and paste this into your coding agent:

```text
Create the Fabric data foundation for a Northwind procurement spend app.
Use the installed Fabric skills for ingestion and semantic-model-authoring
for the model.

Inputs:
- Workbook: data/Northwind_Spend_Extract_FY2026.xlsx
- Alias: <ALIAS>
- Tenant ID: <TENANT_ID>
- Fabric workspace name: <WORKSPACE_NAME>

Ask for any missing inputs. Use my alias in every item name and avoid
changing other participants' items in the shared workspace.

1. Load the workbook:
   Read its README sheet. Create the schema-enabled lakehouse
   northwind_lh_<ALIAS>, upload the workbook to Files/raw/, and create
   and run the notebook load_spend_workbook_<ALIAS>.
   Load Spend_Lines, Suppliers, Categories, Business_Units, and Calendar
   into dbo.spend_lines, dbo.suppliers, dbo.categories, dbo.business_units,
   and dbo.calendar. Make reruns safe for these lab tables.
   Keep IDs and po_number as text and dates as date values.
   Join suppliers by supplier_id, not name, and retain Unmapped categories.
   Validate counts, types, and total spend through the SQL endpoint;
   refresh endpoint metadata and retry if new tables are not yet visible.

2. Create Northwind Spend Model - <ALIAS>:
   Author a complete TMDL model and deploy it using Direct Lake over the
   five lakehouse tables, with partition schemaName: dbo.
   Add many-to-one, single-direction relationships from spend_lines:
   - supplier_id -> suppliers[supplier_id]
   - category_l2 -> categories[category_l2]
   - business_unit -> business_units[business_unit]
   - invoice_date -> calendar[date]
   Mark calendar as the date table, sort month_name by month_number,
   and hide spend_lines[supplier_id], po_number, and invoice_line_id.

3. Add these 15 measures to spend_lines, each with a description:
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

4. Add three RLS roles with read permission:
   - Aerospace only: business_units[business_unit] = "Aerospace Components".
   - BU lead (dynamic): business_units[bu_lead_email] = USERPRINCIPALNAME().
   - Engagement team: no filter.

5. Validate all 15 measures with DAX through the executeQueries API,
   comparing totals and business-unit/category slices with independent
   workbook calculations. Report expected versus actual results.
   Check the role definitions; mark runtime RLS unverified if no Viewer
   test identity is available, since Admin/Member accounts bypass RLS.

Finish by reporting the workspace, lakehouse, notebook, and semantic model
IDs, validation results, and anything that could not be verified.
Stop here. Do not scaffold or build the app yet.
```

## Check the result

| Check | Reference result |
|---|---|
| Total Spend | $1,531,439,208.96 |
| Addressable Spend / % | $1,432,118,289.81 / 93.5% |
| Savings Low / Mid / High | $80,183,266.14 / $118,945,745.12 / $157,708,224.10 |
| Supplier Count / Invoice Lines | 606 / 18,438 |
| Non-PO % / Tail % / Contract Coverage % | 23.4% / 12.4% / 64.2% |
| Unmapped % / Top 10 Supplier Share % | 2.1% / 13.8% |
| Weighted Payment Terms / Spend % of Revenue | 48.1 days / 35.5% |

The model should contain **five tables, four relationships, 15 measures, and three roles**. Compare results with the workbook itself, using the numbers above as a cross-check. Keep the reported model and workspace IDs for the next task.

[Next: Build a visualization](../02-build-visualization/README.md)

[Back to the hackathon](../../../README.md#lets-get-started)
