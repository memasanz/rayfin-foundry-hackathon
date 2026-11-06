# Foundry Dev Pack - macOS

Foundry Dev Pack installs the developer tools for building with Microsoft Foundry. This is separate from the Fabric and Power BI skill installation.

## Before you start

- Install **Visual Studio Code** first if you want the Dev Pack to add the Microsoft Foundry Toolkit extension.
- You need **Homebrew**. If it is unavailable, follow the [official Homebrew installation instructions](https://brew.sh/), where permitted by your organization.
- Use your organization's approved installation process. If installation is blocked, contact the hackathon organizer rather than changing managed settings.

## 1. Install Foundry Dev Pack

Open **Terminal**, or select **Terminal > New Terminal** in VS Code. Run:

```bash
brew install --cask microsoft/foundry/devpack && foundry-devpack install
```

This installs the Dev Pack and then runs its setup. Follow the installer prompts and wait for setup to finish. Review any installation or permission prompts before accepting them.

The Dev Pack installs Foundry command-line tools, including Azure CLI (`az`), Azure Developer CLI (`azd`), the Foundry extensions for `azd`, and the **Microsoft Foundry Skill** for coding agents.

It also installs these integrations when their host apps are present:

| Integration | Required app |
|---|---|
| Microsoft Foundry Toolkit | Visual Studio Code |
| Foundry Canvas (preview) | GitHub Copilot App |

The Dev Pack does **not** install VS Code or GitHub Copilot App.

## 2. Reopen VS Code and verify

Save your work and **fully quit VS Code with Command+Q**, then reopen it so it picks up PATH changes. Open the hackathon folder and a new terminal. Closing a window alone does not necessarily quit VS Code.

Check that the Foundry agent commands are available:

```bash
azd ai agent --help
```

You should see command help rather than a command-not-found error. If the command is still unavailable, follow any PATH instructions printed by the installer or contact the organizer.

In VS Code, look for the **Microsoft Foundry** extension in the Activity Bar or check the Extensions view for **Microsoft Foundry Toolkit**.

Start a **new Copilot chat** and ask:

```text
Can you confirm that the microsoft-foundry skill is available in this session?
Check your available skills and report anything you cannot verify.
Do not install tools, sign in, or create Azure resources.
```

Installation does not sign you in, create Azure resources, or grant access to a Foundry project. Before building, use the Azure subscription and Foundry project provided by the organizer. Git, your application's language runtime, and scenario-specific SDK packages are separate prerequisites.

References: [Foundry Dev Pack announcement](https://devblogs.microsoft.com/foundry/foundry-devpack-announcement/), [official environment setup](https://learn.microsoft.com/azure/foundry/how-to/develop/install-cli-sdk), and [Microsoft Foundry Skill](https://learn.microsoft.com/azure/foundry/how-to/develop/use-microsoft-foundry-skill).

[Back to the hackathon](../../README.md)
