# Agent instructions

These instructions apply to every Rayfin app built in this repository, including apps scaffolded into a subfolder. They describe the hackathon's requirements, not a fixed implementation recipe.

## Use the appropriate guidance

- Read the relevant exercise README before starting. It defines the goal, required inputs, item names, safeguards, and acceptance criteria; skills and templates define the implementation mechanics.
- Scaffold the app first, then read its generated guidance and the relevant installed skills.
- Use the generated app guidance and current official documentation for version-specific implementation details.
- Diagnose the actual failure before introducing a workaround; do not assume that a fix from another app or tool version is required.

## Working style and inputs

- Implement through APIs, CLIs, and files rather than asking the user to perform routine development steps. Ask for human action when interactive sign-in, tenant settings, or explicit approval is required.
- Reuse confirmed inputs from the conversation. Ask only for missing values required by the exercise, and treat unreplaced placeholders as missing. Never invent IDs, endpoints, or credentials.

## App access and live data

- Support both the app's standalone hosting URL in a normal browser tab and its embedded view in the Fabric portal. 
- Set `staticHosting.assetAccess: public`, not `protected`, so the app's static assets and standalone URL are accessible in a normal browser. If the scaffolded template or generated guidance says to keep `staticHosting.assetAccess: protected`, override that setting for this hackathon. Public asset hosting does not grant public access to data; keep the semantic model and APIs authenticated and enforce the signed-in user's permissions.
- Choose authentication and query flows appropriate to each hosting context; do not assume that a Fabric parent frame is always available.
- Keep the semantic model and APIs authenticated, even when the app's static files are publicly accessible.
- Query the live semantic model as the signed-in user. Do not substitute hard-coded totals or copied records for live queries.
- Keep dataset copies out of `src/` and `public/`.
- If a query fails, show a safe error state with its category, message, and request ID when available. Do not replace failed queries with mock data or expose credentials or sensitive diagnostic details.

## Identity and authentication

- Treat Fabric and Foundry sign-in as separate authentication contexts.
- Use the organizer-provided authentication settings and supported sign-in flows that complete successfully in both hosting contexts.
- Preserve the signed-in user's identity and permissions through the app, backend, Foundry, and Fabric IQ. Do not substitute the app owner's identity.
- Keep tokens in memory and client secrets out of browser code.

## Semantic models and validation

- Preserve fixed-decimal precision for monetary totals. Avoid premature rounding in calculations; round for display. Use `DIVIDE` for DAX ratios and explicitly typed non-integer division in SQL and Spark.
- Return `BLANK` when a meaningful result cannot be computed. Preserve genuine zeros; do not force missing or undefined results to zero.
- Batch related live validations against documented control totals and independent source-workbook calculations, not remembered values.
- During reconciliation, accept `BLANK` as zero only for verified no-activity aggregates, not missing data, undefined ratios, or failures.
- When testing an empty selection, verify from the source that it actually has no activity.

## Validate and deploy

- Confirm live connectivity before building the visualizations.
- Validate each phase with an appropriate query, build, test, or CLI check against the exercise's acceptance criteria and any stated control totals. Fix failed checks before continuing; if blocked, report the blocker rather than claiming success.
- Run the app's prescribed build, lint, and tests. Verify sign-in, live data, and user access in both hosting contexts.
- Do not treat local success as proof of deployed identity permissions, or Admin/Member access as proof of Viewer-level row-level security. Verify with the intended user role and hosting context, and report any checks that could not be completed.
- If verification requires an unavailable account, role, or sign-in, report it as "not verified"; do not substitute another identity or work around access controls. Continue only if that check is not a prerequisite for the next step. Otherwise, report the blocker and stop.
- Ask the user to complete interactive sign-in when needed. Do not force deployments without the user's explicit approval.
- Report what was actually verified and any remaining limitations.
- Keep credentials and local environment or deployment files out of Git.
