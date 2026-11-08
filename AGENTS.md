# Agent instructions

These instructions apply to every Rayfin app built in this repository, including apps scaffolded into a subfolder. The generated app's own `AGENTS.md` describes the Fabric iframe client. Use that client inside the Fabric portal. Use the path below for the app's hosting URL.

## Hosting URL and the semantic model

The hosting URL must open in a normal browser tab and query the semantic model as the signed-in user. Do not copy query results, totals, or row data into the frontend. Workspace and model ids stay in `rayfin.yml`.

- Set `services.staticHosting.assetAccess` to `public` so the hosting URL serves the page. Public files do not make the model or the APIs anonymous.
- Inside the Fabric portal, keep the template iframe queries (`useSemanticModelQuery` through the embed client) and `initEmbeddedAuth`.
- On the hosting URL there is no Fabric parent frame. Sign in from a button with `ensureSignedInWithFabric`. `initEmbeddedAuth` returns no session there and must not be the only sign-in path.
- On the hosting URL, run each chart's DAX through a `fabric-semanticmodel` connector named for the model, with `auth.type: delegated`. Register `fabricSemanticModel()` on `ConnectorsRayfinClient`. The browser sends the query text only.
- Prove the connector with one `rayfin connector invoke` before building the charts. Deploy with `npx rayfin up` so the connector is registered. Do not use `npx rayfin up --force` unless the user asks.
- If connector compilation fails with `TS5096` because `allowImportingTsExtensions` is set while `noEmit` is false, set `allowImportingTsExtensions` to false in `rayfin/tsconfig.json` and deploy again.

## Foundry sign-in

Foundry sign-in is separate from the Fabric session above. Use the organizer's single-tenant SPA (PKCE, no client secret) and MSAL `loginPopup`. A full-page redirect does not finish inside the Fabric iframe. Store tokens in `memoryStorage`.

The popup returns to `/auth-callback.html`. That page must call `broadcastResponseToMainFrame` from `@azure/msal-browser/redirect-bridge`. A page with no script never answers the opener, so `loginPopup` fails with `timed_out` (`redirect_bridge_timeout`) after the default 60 seconds.

- Put `auth-callback.html` at the app root and add it to the Vite build input beside `index.html`. Its script calls `broadcastResponseToMainFrame()`.
- Do not add `public/auth-callback.html`. Vite copies `public/` onto the built site and replaces the bridge page with a blank file.
- Register the hosting origin and that origin plus `/auth-callback.html` as SPA redirect URIs. Pass the same redirect URI to `loginPopup`.
- Set `allowRedirectInIframe` to false and `popupBridgeTimeout` above 60 seconds so the user can finish Entra.
- MSAL keeps the in-progress flag in `sessionStorage` under a key containing `interaction.status`. Delete that key before `handleRedirectPromise`. A leftover flag throws `no_token_request_cache_error` or `interaction_in_progress` and the popup never opens. Set `overrideInteractionInProgress` on the popup request.
- Send the signed-in user's Foundry access token (`https://ai.azure.com/user_impersonation`) into the Rayfin function and call Foundry with that token. Do not use the Fabric app-item token. Fabric IQ then runs as that user.
- If sign-in works on the hosting URL and times out only inside the Fabric portal, the popup's BroadcastChannel cannot reach the iframe. That is separate from a blank callback page.

Keep credentials and local environment or deployment files out of Git.
