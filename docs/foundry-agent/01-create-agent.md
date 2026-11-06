# 1. Create and test the Foundry agent

Create a Spend Copilot that answers questions about your existing semantic model before adding it to the app.

## Inputs

Reuse your alias, tenant, Fabric workspace, and semantic model from the app exercises. The organizer supplies a Foundry project endpoint and an available model deployment. For tool installation, see [Foundry Tools](../setup/README.md#foundry-tools).

## Prompt

Replace the placeholders and paste this into your coding agent:

```text
Create a read-only Spend Copilot in Microsoft Foundry for the Northwind
data we used to build the app.

Inputs:
- Alias: <ALIAS>
- Tenant ID: <TENANT_ID>
- Fabric workspace name: <WORKSPACE_NAME>
- Foundry project endpoint: <PROJECT_ENDPOINT>
- Foundry model deployment name: <MODEL_DEPLOYMENT_NAME>

Use the existing semantic model from our app and the installed Foundry
and Fabric skills. Create a Foundry prompt agent named spend-copilot-<ALIAS>
and use my alias for any connection you create.

Use Fabric IQ as its only external tool, connected to our semantic model
with supported delegated-user authentication. The agent should answer
questions about spend, categories, suppliers, and potential savings using
live model evidence, identifying the measures and filters behind its answers.
Treat savings as illustrative benchmarks, not guaranteed savings.

Keep the agent definition and non-secret configuration in our existing
project so we can update it later. Reuse the current data and model.

Test a real question independently of the app, compare the answer with
the model, and share the agent name, version, connection, and test result.
Leave the app unchanged for this step.
```

## Try it

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

[Next: Connect the agent to your Fabric app](02-connect-app.md)

[Back to Build a Foundry Agent](README.md)
