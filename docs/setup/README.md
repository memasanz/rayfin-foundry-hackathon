# 1. Setup Tooling

1. [Local](#local-tools)
2. [Fabric](#fabric-tools)
3. [Foundry](#foundry-tools)

### Local Tools

Install missing tools before the hackathon, starting with **Node.js**, which includes npm. Follow the official instructions for your operating system and obtain any required IT approvals on managed devices. Skip tools that are already installed and meet the requirements. Restart your terminal (and VS Code if you use it) after installation so PATH changes take effect.

| Tool | Requirement | Purpose | Installation | Verify |
|---|---|---|---|---|
| Node.js and npm | Node 20 or later; use a supported LTS release | Rayfin CLI, app builds, and tests | [Node.js](https://nodejs.org/en/download) | `node -v`, `npm -v` |
| Git | Current | Clone the hackathon repository | [Git](https://git-scm.com/install/) | `git --version` |
| Azure CLI | Current | Entra tokens for Fabric, Power BI, OneLake, and SQL | [Azure CLI](https://learn.microsoft.com/cli/azure/install-azure-cli) | `az version` |
| Python | 3.10 or later | Agent tasks such as reading Excel files and calling REST APIs | [Python](https://www.python.org/downloads/) | `python --version` |
| Azure Functions Core Tools | v4; required for Foundry agent integration | Generate function types with `npx rayfin dev functions apply` | [Core Tools](https://learn.microsoft.com/azure/azure-functions/functions-run-local#install-the-azure-functions-core-tools) | `func --version` |

On macOS, use `python3 --version` if `python` is unavailable.

#### Check your local tools with your coding agent

Open the hackathon folder in your coding agent and paste:

```text
Check whether my computer has the local tools needed for this hackathon.
Read the Local Tools and Rayfin setup sections of the Setup Tooling guide
in this repository and use their requirements.

Detect my operating system and shell. Run version and PATH checks for
Node.js, npm, Git, Azure CLI, Python, and Azure Functions Core Tools.
If python is unavailable, try python3 on macOS or py -3 on Windows.
Compare the installed versions with the stated requirements.
Run npm view @microsoft/create-rayfin version to check package access
through my configured npm registry. Do not override the registry or assume
that npm ping is supported by a corporate proxy.

Do not install or update anything, change settings, sign in, or deploy
resources. Do not print tokens, secrets, or environment-variable values.
Do not treat the absence of a globally installed Rayfin CLI as a failure:
Rayfin is run through npm create and npx.

Return a short table: tool, installed version, pass/fail/unknown, and
next action. Report the actual command results, not assumed availability.
For missing or incompatible tools, link to the installation instructions
in this guide. Finish with whether my local prerequisites are ready.
Keep this separate from Fabric/Foundry permissions and connectivity.
```

#### Rayfin setup

No separate `npm install rayfin` step is needed. With Node.js/npm installed, let your coding agent scaffold the app and install its project dependencies using the Rayfin guidance. Rayfin uses `npm create` for scaffolding and `npx rayfin` for CLI commands. Your npm must be able to retrieve the required packages through your organization's approved registry, or the public npm registry where permitted.

On managed devices, use the registry approved by your IT team. If package access is blocked, contact IT rather than bypassing policy. A successful package metadata check confirms access to that package, not that every app dependency is available.

**Azure Functions Core Tools is a separate prerequisite**, not supplied by Rayfin or Foundry Dev Pack.

### Fabric Tools

Choose your tool and operating system:

| Tool | Windows | macOS |
|---|---|---|
| GitHub Copilot in VS Code | [Windows setup](../install/github-copilot-windows.md) | [macOS setup](../install/github-copilot-macos.md) |
| Cursor IDE | [Windows setup](../install/cursor-windows.md) | [macOS setup](../install/cursor-macos.md) |
| Claude Code | [Windows setup](../install/claude-desktop-windows.md) | [macOS setup](../install/claude-desktop-macos.md) |

### Foundry Tools

Install **Foundry Dev Pack** for Foundry command-line tools, the Microsoft Foundry Skill, and editor integrations. This is separate from the Fabric and Power BI skills above. See Microsoft's official [Prepare your development environment](https://learn.microsoft.com/en-us/azure/foundry/how-to/develop/install-cli-sdk?tabs=windows%2Cpython%2Cazd-ai) guide for details.

| Tool | Windows | macOS |
|---|---|---|
| Foundry Dev Pack | [Windows setup](../install/foundry-devpack-windows.md) | [macOS setup](../install/foundry-devpack-macos.md) |

#### Confirm your installed skills

Use this check whether your skills were installed earlier or just now. Open a **new chat** in your coding agent with the hackathon folder open and paste:

```text
Check whether these skills are available in this session:
- semantic-model-authoring
- powerbi-report-cli
- microsoft-foundry

Use your available skill list and report each as available, missing,
or unable to verify. Do not assume availability from general knowledge.
Do not install or update anything, invoke skill workflows, or change settings.
```

If a skill is missing, use the relevant installation guide above. This checks skill availability, not authentication or live Fabric/Foundry connectivity.

[Next: Build our App](../build-app/README.md)

[Back to the hackathon](../../README.md)