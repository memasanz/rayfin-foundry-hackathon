# 2. Build our App

Turn a synthetic procurement workbook into a live Fabric app for exploring spend and illustrative savings opportunities.

**What you will build:** Excel workbook -> schema-enabled lakehouse -> Direct Lake semantic model -> four-page Rayfin app.

## How to work through the lab

Complete [Setup Tooling](../setup/README.md), then open the hackathon folder in your coding agent.

1. [Create a semantic model in Fabric](../getting-started/01-semantic-model/README.md) - Confirm inputs, load the workbook, and build and validate the model.
2. [Build a visualization](../getting-started/02-build-visualization/README.md) - Scaffold the app, connect to the model, build its pages, and deploy.

Each section has a short prompt and a **checkpoint**. Paste one prompt at a time, review the result, and continue only after the checkpoint passes. The agent must stop between sections rather than run the whole lab at once.

Use the **same chat and workspace** throughout. If you start a new chat, provide this page, the exercise page, your confirmed inputs, and the item IDs reported at the last checkpoint. Do not paste tokens or credentials.

## Inputs

Download the synthetic [Northwind Spend workbook](https://github.com/jennyney5/rayfin-hackathon-starter/blob/main/data/Northwind_Spend_Extract_FY2026.xlsx) using **Download raw file**, create a `data` folder at this repository's root, and save it there as `Northwind_Spend_Extract_FY2026.xlsx`. The workbook is not bundled in this repository.

Have these values ready:

| Input | What to provide |
|---|---|
| Workbook | `data/Northwind_Spend_Extract_FY2026.xlsx`, relative to the repository root |
| Alias | A short lowercase alias using letters and numbers, unique within the workspace |
| Tenant ID | The hackathon tenant supplied by the organizer |
| Workspace name | The team's workspace on an active Fabric capacity; you need Admin or Member access |

Use only this synthetic workbook, not client or personal data.

## Lab guardrails

These rules apply to every prompt in the app-building exercises:

- Ask for missing inputs and workbook-path confirmation before reading or importing the workbook or creating resources. Never guess IDs, endpoints, or alternative data sources.
- Use alias-suffixed names: `northwind_lh_<ALIAS>`, `load_spend_workbook_<ALIAS>`, `Northwind Spend Model - <ALIAS>`, and `spend-diagnostic-<ALIAS>`. List existing items first. Reuse only verified items belonging to this lab and alias; ask before replacing existing content. Never modify or delete another participant's items.
- Read the installed Fabric skills before Fabric work. Use `semantic-model-authoring` for the model. For app work, scaffold first, then read the generated `AGENTS.md` and relevant `.agents/skills/` before implementation. Follow that generated guidance for version-specific commands and connector wiring.
- Keep the generated Fabric sign-in flow and `staticHosting.assetAccess: protected`. Do not put workbook files in `src` or `public`, or put tokens, secrets, or direct Power BI REST calls in front-end code. Never commit `rayfin/.env`, `rayfin/.deployments.json`, `.env.local`, or credentials.
- Use live model queries, not mock data or hard-coded business numbers. Show loading, empty, and error states; errors should include category, message, and request ID when available.
- Do not use forced deployment or encryption fallbacks without explicit approval. Ask the participant to complete interactive sign-ins; do not change tenant settings, permissions, or managed-device settings automatically.
- Validate each phase before continuing. Compare results with calculations from the confirmed workbook, not just the reference numbers in this guide. Report failures and unverified checks plainly, and stop at the current checkpoint.

This lab adapts [Scenario 1: Spreadsheet to App](https://github.com/jennyney5/rayfin-hackathon-starter/tree/main/scenario-1-spreadsheet-to-app) into participant-controlled steps. Visualization changes, writeback, and the Foundry agent are later exercises, not part of this initial build.

[Previous: Setup Tooling](../setup/README.md) | [Next: Update our App](../update-app/README.md)

[Back to the hackathon](../../README.md)
