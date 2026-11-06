# 1. Create a semantic model in Fabric

Create and validate the data foundation before building the app. Follow the [lab overview and guardrails](../../build-app/README.md) first.

## 1.1 Confirm your inputs and sign in

Download the workbook and collect the inputs listed in the overview. Open a terminal in the repository root and sign in yourself:

```text
az login --tenant <TENANT_ID>
```

Replace `<TENANT_ID>` with the organizer's tenant ID. This is interactive; do not paste sign-in tokens into chat.

Replace the placeholders in this prompt, then paste it into your coding agent:

```text
Read docs/build-app/README.md, including the lab guardrails, and
docs/getting-started/01-semantic-model/README.md.
Work only on section 1.1, not the whole lab.

My inputs:
- Workbook: data/Northwind_Spend_Extract_FY2026.xlsx
- Alias: <ALIAS>
- Tenant ID: <TENANT_ID>
- Fabric workspace name: <WORKSPACE_NAME>

Check for missing inputs and validate that the alias is lowercase letters
and numbers. Check that the workbook exists, then ask me to confirm its path
before reading it or creating resources.

After confirmation, use the installed Fabric skills to verify my signed-in
tenant, workspace access, and active capacity. Discover the workspace ID
and list any existing items matching my alias. Do not change permissions
or tenant settings, and do not print access tokens.

Report the confirmed inputs, workspace ID, and planned item names.
Do not create a lakehouse, model, or app yet. Stop for my review.
```

**Checkpoint:** You have confirmed the workbook, tenant, alias, workspace ID, and access. Resolve missing inputs or permissions with the organizer before continuing.

## 1.2 Load the workbook into a lakehouse

The workbook contains five data sheets and a `README` sheet with definitions and data-quality notes.

| Sheet | Target table in `dbo` | Reference row count |
|---|---|---|
| `Spend_Lines` | `spend_lines` | 18,438 |
| `Suppliers` | `suppliers` | 606 |
| `Categories` | `categories` | 25 |
| `Business_Units` | `business_units` | 4 |
| `Calendar` | `calendar` | 365 |

Paste this next:

```text
Continue with section 1.2 only, using my confirmed inputs and lab guardrails.

Read the workbook's README sheet, then inspect the five data sheets.
Calculate source row counts and total invoice_amount_usd from the workbook.

Use the Fabric skills to create the schema-enabled lakehouse
northwind_lh_<ALIAS>, upload the confirmed workbook to Files/raw/, and
create and run load_spend_workbook_<ALIAS>. Replace <ALIAS> with my
confirmed alias. Load the five sheets into the dbo tables listed in this guide.
Use safe, repeatable overwrite behavior only for these confirmed lab tables.

Preserve IDs and po_number as text, and invoice_date and calendar date
as dates. Suppliers must be identified by supplier_id, not supplier name.
Preserve and report the Unmapped category rather than dropping its rows.

Validate table row counts, column types, and total spend through the SQL
analytics endpoint against the workbook. If new tables are missing there,
refresh endpoint metadata and retry before treating the load as failed.

Report source-versus-loaded results, lakehouse and notebook IDs, and
anything unverified. Do not create the semantic model or scaffold an app.
Stop for my review.
```

**Checkpoint:** All five tables are visible through the SQL endpoint, counts and spend reconcile to the workbook, and key/date types are correct. The original workbook's reference total is **$1,531,439,208.96**; investigate differences instead of hard-coding that value.

## 1.3 Create the semantic model

### Model requirements

Use Direct Lake over all five tables in `northwind_lh_<ALIAS>`, with partition `schemaName: dbo`.

| From | To | Relationship |
|---|---|---|
| `spend_lines[supplier_id]` | `suppliers[supplier_id]` | Many-to-one, single direction |
| `spend_lines[category_l2]` | `categories[category_l2]` | Many-to-one, single direction |
| `spend_lines[business_unit]` | `business_units[business_unit]` | Many-to-one, single direction |
| `spend_lines[invoice_date]` | `calendar[date]` | Many-to-one, single direction |

Mark `calendar` as the date table, sort `calendar[month_name]` by `month_number`, and hide `spend_lines[supplier_id]`, `po_number`, and `invoice_line_id`.

Create these **15 measures** on `spend_lines`, each with a description and format string:

| Measure | Definition | Format |
|---|---|---|
| Total Spend | Sum of invoice amounts in USD | `$#,0.0,,"M"` |
| Addressable Spend | Spend in addressable categories | `$#,0.0,,"M"` |
| Addressable % | Addressable Spend / Total Spend | `0.0%` |
| Savings Opportunity Low | Category spend multiplied by its low savings percentage | `$#,0.0,,"M"` |
| Savings Opportunity Mid | Average of low and high savings opportunities | `$#,0.0,,"M"` |
| Savings Opportunity High | Category spend multiplied by its high savings percentage | `$#,0.0,,"M"` |
| Supplier Count | Distinct suppliers with spend | `#,0` |
| Invoice Lines | Invoice-line count | `#,0` |
| Non-PO Spend % | Share of spend with `po_flag = Non-PO` | `0.0%` |
| Tail Spend % | Share of spend with Tail-tier suppliers | `0.0%` |
| Contract Coverage % | Share of spend with contracted suppliers | `0.0%` |
| Unmapped Spend % | Share of spend in the Unmapped category | `0.0%` |
| Top 10 Supplier Share % | Share of spend with the ten largest suppliers | `0.0%` |
| Weighted Payment Terms (days) | Payment terms weighted by invoice amount | `0.0` |
| Spend % of Revenue | Spend / business-unit revenue, with matching currency units | `0.0%` |

Savings percentages must use the workbook's units and each category's own rate. Do not apply a global maximum rate to every category. Business-unit revenue is recorded in millions of dollars, so convert units before calculating Spend % of Revenue.

Add three RLS roles with read permission:

| Role | Filter |
|---|---|
| Aerospace only | `business_units[business_unit] = "Aerospace Components"` |
| BU lead (dynamic) | `business_units[bu_lead_email] = USERPRINCIPALNAME()` |
| Engagement team | No filter |

Paste this next:

```text
Continue with section 1.3 only, using the validated lakehouse and lab guardrails.
Read the installed semantic-model-authoring skill before model work.

Author Northwind Spend Model - <ALIAS> as TMDL, replacing <ALIAS> with
my confirmed alias. Follow all model requirements in this guide:
Direct Lake, five dbo tables, four relationships, date-table configuration,
hidden keys, 15 described/formatted measures, and three read-permission RLS roles.

Author the complete model before the initial deployment, then deploy once.
Validate deployment and read back model metadata. If something fails,
report it and repair only the affected lab artifacts.

Report the semantic model ID, table and measure inventory, relationships,
and role definitions. Do not scaffold an app. Stop for my review.
```

**Checkpoint:** The model is deployed with five tables, four relationships, all 15 measures, and three roles. Role creation alone does not prove RLS works for an end user.

## 1.4 Validate the model before building

Paste this next:

```text
Continue with section 1.4 only. Follow the lab guardrails.

Use the installed semantic-model guidance to validate all 15 measures with
DAX through the Power BI executeQueries API. Independently calculate their
expected results from the confirmed workbook. Check both totals and
business-unit/category slices so relationship or filter errors are visible.

Report expected versus actual values, differences, and rounding tolerances.
Verify the role definitions. Do not claim runtime RLS validation from my
Admin/Member account: those workspace roles are not filtered by RLS.
If a suitable Viewer test identity is unavailable, mark runtime RLS unverified.

If Execute Queries is disabled or access is denied, stop and identify the
organizer action needed. Do not change tenant settings automatically.
Do not build the app until required data and measure checks pass.
Stop for my review and provide the model ID for the next exercise.
```

The source lab reports these reference results for its workbook:

| Check | Reference result |
|---|---|
| Total Spend | $1,531,439,208.96 |
| Addressable Spend / % | $1,432,118,289.81 / 93.5% |
| Savings Low / Mid / High | $80,183,266.14 / $118,945,745.12 / $157,708,224.10 |
| Supplier Count / Invoice Lines | 606 / 18,438 |
| Non-PO % / Tail % / Contract Coverage % | 23.4% / 12.4% / 64.2% |
| Unmapped % / Top 10 Supplier Share % | 2.1% / 13.8% |
| Weighted Payment Terms / Spend % of Revenue | 48.1 days / 35.5% |

**Checkpoint:** All 15 measures reconcile to workbook calculations. Any RLS testing limitation is explicitly recorded. Keep the confirmed lakehouse and model IDs for the app exercise.

[Next: Build a visualization](../02-build-visualization/README.md)

[Back to the hackathon](../../../README.md#lets-get-started)
