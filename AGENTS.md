# Agent instructions

These instructions apply to every Rayfin app built in this repository, including apps scaffolded into a subfolder. They describe the hackathon's requirements, not a fixed implementation recipe.

## Use the appropriate guidance

- Scaffold the app first, then read its generated guidance and the relevant installed skills.
- Use the generated app guidance and current official documentation for version-specific implementation details.
- Diagnose the actual failure before introducing a workaround; do not assume that a fix from another app or tool version is required.

## App access and live data

- Support both the app's standalone hosting URL in a normal browser tab and its embedded view in the Fabric portal. 
- Set `staticHosting.assetAccess: public`, not `protected`, so the app's static assets and standalone URL are accessible in a normal browser. If the scaffolded template or generated guidance says to keep `staticHosting.assetAccess: protected`, override that setting for this hackathon. Public asset hosting does not grant public access to data; keep the semantic model and APIs authenticated and enforce the signed-in user's permissions.
- Choose authentication and query flows appropriate to each hosting context; do not assume that a Fabric parent frame is always available.
- Keep the semantic model and APIs authenticated, even when the app's static files are publicly accessible.
- Query the live semantic model as the signed-in user. Do not substitute hard-coded totals or copied records for live queries.

## Identity and authentication

- Treat Fabric and Foundry sign-in as separate authentication contexts.
- Use the organizer-provided authentication settings and supported sign-in flows that complete successfully in both hosting contexts.
- Preserve the signed-in user's identity and permissions through the app, backend, Foundry, and Fabric IQ. Do not substitute the app owner's identity.
- Keep tokens in memory and client secrets out of browser code.

## Validate and deploy

- Confirm live connectivity before building the visualizations.
- Run the app's prescribed build, lint, and tests. Verify sign-in, live data, and user access in both hosting contexts.
- Ask the user to complete interactive sign-in when needed. Do not force deployments without the user's explicit approval.
- Report what was actually verified and any remaining limitations.
- Keep credentials and local environment or deployment files out of Git.
