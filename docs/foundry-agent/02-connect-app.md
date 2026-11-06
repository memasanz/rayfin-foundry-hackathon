# 2. Connect the agent to your Fabric app

Add a Spend Copilot chat panel alongside the app's existing dashboards.

**How it connects:** App -> authenticated Rayfin Function -> Foundry agent -> Fabric IQ -> your semantic model.

## Before connecting

The organizer supplies an approved **single-tenant SPA client ID** with delegated Foundry access (`https://ai.azure.com/user_impersonation`) and any required consent. They must register your app's actual deployed HTTPS root URL as a SPA redirect URI. Use the hosting URL, not the Fabric portal URL.

Each user needs permission to invoke the agent and access the model. The Foundry sign-in is separate from the dashboard's Fabric sign-in. No client secret is needed.

The functions workflow requires **Azure Functions Core Tools v4** on the development machine. Install it if missing using the [official instructions](https://learn.microsoft.com/azure/azure-functions/functions-run-local#install-the-azure-functions-core-tools).

## Prompt

Continue in the same chat and replace the client ID:

```text
Connect the Spend Copilot we just created to our existing Fabric app.

Inputs:
- Organizer-supplied SPA client ID: <SHARED_SPA_CLIENT_ID>

Reuse our app project, alias, tenant, workspace, semantic model, Foundry
project endpoint, and agent name. Use the generated Rayfin guidance and
installed Foundry skills for the implementation.

Add a responsive Spend Copilot panel alongside the four existing tabs.
Include a question box and starter questions: "Explain this view",
"What should we investigate next?", and "Summarize for SteerCo".
Keep the app's existing design and dashboards.

Add Connect to Foundry, Change account, and Disconnect controls using
the organizer's SPA registration. Show the connected Foundry account.
Use supported MSAL sign-in with PKCE and memory-only token storage,
including the supported popup flow when the app is embedded in Fabric.
Ask the organizer to register the actual app-root callback if needed.

Connect through an authenticated Rayfin Function using the signed-in
user's Foundry identity. Preserve their permissions when querying Fabric IQ.

Pass the current tab and business-unit selection to the agent as context.
Display its answers and references in the chat panel.

Make the chat responsive, with formatted answers, loading feedback,
and retryable errors. Prevent duplicate sends. Keep tokens and chat
in memory only, and reset the conversation when the account or view changes
without showing late responses from the previous context.

Test the integration, run the project's build, lint, and tests, then deploy
to the same Fabric App item. Share the URL and what you verified.
```

## Check the result

Open the deployed app **inside Fabric** and:

1. Connect to Foundry and confirm the selected account.
2. Ask "What is our total spend?" and compare with the model for that user.
3. Select Aerospace Components and ask "Explain this view".
4. Confirm the answer uses that scope and includes model-derived evidence.
5. Disconnect or change accounts and confirm the previous chat clears.
6. Confirm all four dashboard tabs still work.

Also try canceling sign-in and retrying. Record any checks you could not complete. An Admin or Member test does not prove Viewer-level RLS isolation.

[Previous: Create and test the Foundry agent](01-create-agent.md)

[Next: Create a writeback](../getting-started/04-writeback/README.md)

[Back to Build a Foundry Agent](README.md)
