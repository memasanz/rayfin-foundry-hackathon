# Northwind procurement spend dataset

[Northwind_Spend_Extract_FY2026.xlsx](Northwind_Spend_Extract_FY2026.xlsx) is a synthetic accounts-payable dataset for the fictional **Northwind Industrial Group**. It supports the hackathon's spend diagnostic app, Fabric semantic model, and Foundry Spend Copilot.

**Training data only:** company and supplier names, contacts, amounts, and savings ranges are illustrative. Email addresses use the reserved `.example` domain. This is not a real company's extract or a source of validated procurement benchmarks.

## Coverage and control totals

The workbook represents invoice-line-level spend for **January 1 through December 31, 2026**, with an illustrative extract date of January 15, 2027.

| Check | Expected value |
|---|---|
| Invoice lines | 18,438 |
| Total spend (`invoice_amount_usd`, rounded to cents) | USD 1,531,439,208.96 |
| Suppliers in the master | 606 |
| Level-2 categories | 25 |
| Business units | 4 |
| Calendar dates | 365 |

Amounts are expressed in USD; the workbook describes them as converted at monthly average exchange rates. These totals are ingestion checks, not values to hard-code into the app.

## Workbook sheets

The workbook contains a `README` sheet with a data dictionary and data-quality notes, plus five data sheets. Each data sheet has column headers in row 1 and records starting in row 2, formatted as an Excel table named `tbl_<SheetName>`.

| Sheet | Grain and purpose | Key |
|---|---|---|
| `Spend_Lines` | One row per invoice line; spend amount, posting date, business unit, site, supplier, category, purchase order, and payment terms | `invoice_line_id` |
| `Suppliers` | One row per supplier; country, primary category, tier, contract status, and diverse-supplier flag | `supplier_id` |
| `Categories` | One row per level-2 category; taxonomy, category type, addressability, savings ranges, and primary savings lever | `category_l2` |
| `Business_Units` | One row per business unit; code, region, annual revenue, and fictional lead contact | `business_unit` |
| `Calendar` | One row per day in 2026; year, quarter, month, and year-month labels | `date` |

## How the tables relate

Use `Spend_Lines` as the fact table, with many-to-one relationships to the four dimension tables:

| Invoice-line column | Dimension column |
|---|---|
| `Spend_Lines.supplier_id` | `Suppliers.supplier_id` |
| `Spend_Lines.category_l2` | `Categories.category_l2` |
| `Spend_Lines.business_unit` | `Business_Units.business_unit` |
| `Spend_Lines.invoice_date` | `Calendar.date` |

Use supplier IDs rather than supplier names to identify legal entities. A supplier's `primary_category_l2` describes its main category; use the invoice line's `category_l2` for spend categorization.

## Important fields and units

| Field | Meaning and handling |
|---|---|
| `invoice_amount_usd` | Invoice-line spend in dollars; sum this field for total spend |
| `invoice_date`, `Calendar.date` | Excel dates; load as date values, not raw Excel serial numbers |
| `invoice_line_id`, `supplier_id`, `po_number` | Text identifiers; preserve them as text, including digit-only purchase-order numbers |
| `po_flag` | `PO` or `Non-PO`; purchase-order numbers are blank for non-PO lines |
| `payment_terms_days` | Payment terms in days; use spend weighting when calculating weighted average terms |
| `supplier_tier` | `Strategic`, `Preferred`, `Approved`, or `Tail`, assigned by FY2026 spend rank |
| `contract_status` | `Under contract` or `No contract` |
| `diverse_supplier` | `Y` or `N` |
| `category_type` | `Direct`, `Indirect`, `Non-addressable`, or `Unclassified` |
| `addressable` | `Yes` or `No`; indicates whether a category is considered addressable for the exercise |
| `savings_low_pct`, `savings_high_pct` | Whole-number percentage units: `6` means 6%, so divide by 100 before multiplying by spend |
| `revenue_usd_m` | Annual business-unit revenue in millions of dollars; multiply by 1,000,000 before comparing with spend in dollars |
| `bu_lead_email` | Fictional contact for row-level-security demonstrations, not an actual sign-in identity |

## Data-quality notes and interpretation

- About 2% of spend is categorized as `Unmapped`, with `category_l1 = Unclassified`. Retain it in total spend and expose it as a classification gap rather than silently dropping it.
- Missing purchase-order numbers on `Non-PO` lines are intentional.
- Supplier trading names may repeat across countries or legal entities; joining by name can produce incorrect results.
- Savings ranges are illustrative opportunities, not committed or realized savings. Calculate low and high opportunities using each category's own spend and rate; do not apply one flat rate to all spend.

The dataset supports questions about spend by business unit, category, supplier, and month; supplier concentration; contract coverage; non-PO and tail spend; payment terms; and illustrative savings opportunities.

## Use in the hackathon

Follow [Build our App](../docs/build-app/README.md) to load the five data sheets into a schema-enabled Fabric lakehouse, build and validate a Direct Lake semantic model, and connect the app to live authenticated queries. The workbook's `README` sheet is documentation, not a sixth data table.
