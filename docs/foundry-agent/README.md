# 3. Build a Foundry Agent

Add a Spend Copilot to the Fabric app you built earlier.

1. [Create and test the Foundry agent](#1-create-and-test-the-foundry-agent) - Connect an agent to your semantic model and ask it questions.
2. [Connect the agent to your Fabric app](#2-connect-the-agent-to-your-fabric-app) - Add a chat panel to the existing app.

Continue in the same chat and app project. Each step has a prompt and a short check before moving on.

## 1. Create and test the Foundry agent

Create a Spend Copilot that answers questions about your existing semantic model before adding it to the app.

### Inputs

Reuse your alias, tenant, Fabric workspace, and semantic model from the app exercises. The organizer supplies a Foundry project endpoint and an available model deployment. For tool installation, see [Foundry Tools](../setup/README.md#foundry-tools).

### Agent creation prompt

Replace the placeholders and paste this into your coding agent:

```text
Create a read-only Spend Copilot in Microsoft Foundry using our existing
Northwind semantic model, with Fabric IQ as its only external tool.
Use the installed skills and my alias for agent and connection names.

Answers should use live model evidence, respect the connected user's
permissions and requested business-unit filters, and cite the measures
and scope used. Describe savings as illustrative benchmarks.

Inputs:
- Alias: <ALIAS>
- Tenant ID: <TENANT_ID>
- Fabric workspace name: <WORKSPACE_NAME>
- Foundry project endpoint: <PROJECT_ENDPOINT>
- Foundry model deployment name: <MODEL_DEPLOYMENT_NAME>

Save the agent definition in our existing project. Test a spend question
against the model and report the result, agent name, and version.
Leave the app unchanged.
```

### Try it

Ask the agent:

```text
What is our total spend, and which business unit has the highest spend?
```

Then ask:

```text
For Aerospace Components, which categories have the largest illustrative
savings opportunities?
```

Check that answers come from your model, the business-unit filter is applied, and the figures agree with the model's results for the test user. If access or consent is missing, have the organizer resolve it before moving on.

Keep the reported agent name and Foundry project endpoint for the next step.

## 2. Connect the agent to your Fabric app

Add a Spend Copilot chat panel alongside the app's existing dashboards.

**How it connects:** App -> authenticated Rayfin Function -> Foundry agent -> Fabric IQ -> your semantic model.

### Before connecting

The organizer supplies an approved **single-tenant SPA client ID** with delegated Foundry access (`https://ai.azure.com/user_impersonation`) and any required consent. They must register your app's actual deployed HTTPS root URL as a SPA redirect URI. Use the hosting URL, not the Fabric portal URL.

Each user needs permission to invoke the agent and access the model. The Foundry sign-in is separate from the dashboard's Fabric sign-in. No client secret is needed.

The functions workflow requires **Azure Functions Core Tools v4** on the development machine. Install it if missing using the [official instructions](https://learn.microsoft.com/azure/azure-functions/functions-run-local#install-the-azure-functions-core-tools).

### App integration prompt

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

### Check the integration

Open the deployed app **inside Fabric** and:

1. Connect to Foundry and confirm the selected account.
2. Ask "What is our total spend?" and compare with the model for that user.
3. Select Aerospace Components and ask "Explain this view".
4. Confirm the answer uses that scope and includes model-derived evidence.
5. Disconnect or change accounts and confirm the previous chat clears.
6. Confirm all four dashboard tabs still work.

Also try canceling sign-in and retrying. Record any checks you could not complete. An Admin or Member test does not prove Viewer-level RLS isolation.

[Previous: Build our App](../build-app/README.md) | [Next: Update our App](../update-app/README.md)

[Back to the hackathon](../../README.md)
