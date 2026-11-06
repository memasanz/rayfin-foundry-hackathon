# 2. Build a visualization

Build a Rayfin app using the semantic model from [exercise 1](../01-semantic-model/README.md). Continue in the same chat so the agent has your alias, workspace, and model details.

You do not need to run `npm install rayfin` first. The agent will scaffold the app and install its project dependencies using the Rayfin guidance.

## Pick your prompt

Choose **one** option and paste it into your coding agent:

| Option | Approach |
|---|---|
| [Let the agent decide](#option-1-let-the-agent-decide) | Name the four tabs and design style; let the agent choose the visuals and implementation. |
| [Detailed instructions](#option-2-detailed-instructions) | Specify the app setup, visuals for each tab, validation, and deployment. |

## Option 1: Let the agent decide

```text
Build and deploy a Rayfin app using the semantic model we just created.
Use my alias in the app name.

Build a polished UI with four tabs: Executive overview, Category deep-dive,
Supplier concentration, and Opportunity. Choose useful visuals for each
tab based on the model and connect them to live data.

Design: white surfaces, navy headers #0E1E3D, one accent #0078D4,
$M and % to one decimal, loading, empty and error states on every visual
(errors show category, message and request ID), readable at 1366 px.
```

## Option 2: Detailed instructions

```text
Build and deploy a Northwind procurement spend app using the Fabric
semantic model we created in the previous task. Use my existing alias,
tenant, workspace, and model IDs; ask for anything missing.

Scaffold spend-diagnostic-<ALIAS> from the Rayfin dataapp template in
my workspace. Scaffold first, then read the generated AGENTS.md and
relevant .agents/skills/. Follow them for version-specific setup,
dependencies, connector registration, query validation, app code,
and deployment. Use my alias so the app does not collide with others.

Register a fabric-semanticmodel connector named spendmodel for the
existing model. Prove live connectivity, discover its schema, and read
measure descriptions before writing queries. Map the requirements below
to the actual model. If a necessary measure is missing, use the
semantic-model-authoring skill to add and validate it in my model.
Validate every final app query with the template-prescribed tools.

Build four tabs, all using live model queries with no mock or
hard-coded business numbers:

1. Executive overview:
   - KPI cards for Total Spend, Addressable Spend, Addressable %,
     and Savings Opportunity Mid.
   - Spend by business unit.
   - Spend by month using calendar[year_month], in chronological order.
   - A three-bullet "So what" panel computed from query results, not an LLM.

2. Category deep-dive:
   - Top 15 category_l2 values by spend, colored by category_l1.
   - Business unit by category_l1 heatmap.
   - Savings range by category_l1.

3. Supplier concentration:
   - Pareto chart of the top 50 suppliers.
   - Spend by supplier tier.
   - Top-25 supplier grid.
   Identify suppliers by supplier_id, since names can repeat.

4. Opportunity:
   - Waterfall from Addressable Spend to Mid savings by primary_lever.
   - Category table flagging fragmentation where more than 40 suppliers
     have spend in the category.

Design: white surfaces, navy headers #0E1E3D, one accent #0078D4,
$M and % to one decimal, loading, empty and error states on every visual
(errors show category, message and request ID), readable at 1366 px.
Label every savings figure as an illustrative benchmark.

Keep staticHosting.assetAccess: protected and the template's Fabric
sign-in flow. Keep credentials and local environment/deployment files
out of Git. Ask me to complete interactive Rayfin sign-in when needed.
Do not use npx rayfin up --force without asking me.

Run the template-prescribed build, lint, and tests, then deploy with
npx rayfin up and capture the actual hostingUrl from deployment status.
Verify that key totals and slices match the workbook-derived results
from the previous task through both model DAX and connector queries.

Report the App item ID, hostingUrl, what you verified with the numbers,
and anything you could not verify.
```

## Check the result

Open the app URL and sign in. Check that all four tabs load live data, the numbers agree with your model, and the design is readable at 1366 px. Keep this app for the next exercise.

[Previous: Create a semantic model in Fabric](../01-semantic-model/README.md) | [Next: Change the visualization](../03-change-visualization/README.md)

[Back to the hackathon](../../../README.md#lets-get-started)
