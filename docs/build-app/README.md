# 2. Build our App

Turn a synthetic procurement workbook into a live Fabric app for exploring spend and illustrative savings opportunities.

**What you will build:** Excel workbook -> schema-enabled lakehouse -> Direct Lake semantic model -> four-page Rayfin app.

## How to work through the lab

Open the hackathon folder in your coding agent.

1. [Create a semantic model in Fabric](../getting-started/01-semantic-model/README.md) - Confirm inputs, load the workbook, and build and validate the model.
2. [Build a visualization](../getting-started/02-build-visualization/README.md) - Scaffold the app, connect to the model, build its pages, and deploy.
3. [Change the visualization](../getting-started/03-change-visualization/README.md) - Update a chart in the app and deploy the change.

The first two exercises offer a simple goal-based prompt and a detailed prompt; choose one. Then use the visualization-change prompt to refine your app. Review each result before continuing.

Use the **same chat and workspace** throughout. If you start a new chat, provide this page, the exercise page, your confirmed inputs, and the item IDs reported at the last checkpoint. Do not paste tokens or credentials.

## Inputs

Use the synthetic [Northwind Spend workbook](../../data/Northwind_Spend_Extract_FY2026.xlsx) included in this repository at `data/Northwind_Spend_Extract_FY2026.xlsx`. No separate download is needed.

Have these values ready:

| Input | What to provide |
|---|---|
| Workbook | `data/Northwind_Spend_Extract_FY2026.xlsx`, relative to the repository root |
| Alias | A short lowercase alias using letters and numbers, unique within the workspace |
| Tenant ID | The hackathon tenant supplied by the organizer |
| Workspace name | The team's workspace on an active Fabric capacity; you need Admin or Member access |

## Item names

Your alias keeps your work separate from other participants in the shared workspace:

| Item | Name |
|---|---|
| Lakehouse | `northwind_lh_<ALIAS>` |
| Notebook | `load_spend_workbook_<ALIAS>` |
| Semantic model | `Northwind Spend Model - <ALIAS>` |
| App | `spend-diagnostic-<ALIAS>` |

Use your own items and check before replacing existing work. Let the agent use the installed Fabric skills and the app's generated guidance for implementation details.

[Previous: Setup Tooling](../setup/README.md) | [Next: Update our App](../update-app/README.md)

[Back to the hackathon](../../README.md)
