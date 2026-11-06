# 1. Create and test the Foundry agent

Create a Spend Copilot that answers questions about your existing semantic model before adding it to the app.

## Inputs

Reuse your alias, tenant, Fabric workspace, and semantic model from the app exercises. The organizer supplies a Foundry project endpoint and an available model deployment. For tool installation, see [Foundry Tools](../setup/README.md#foundry-tools).

## Prompt

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
