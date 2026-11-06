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
| Azure Functions Core Tools | v4; required for starter scenarios 1b and 2 | Generate function types with `npx rayfin dev functions apply` | [Core Tools](https://learn.microsoft.com/azure/azure-functions/functions-run-local#install-the-azure-functions-core-tools) | `func --version` |

On macOS, use `python3 --version` if `python` is unavailable.

Rayfin is fetched through `npx` and `npm create`; no global Rayfin installation is needed. Your npm must be able to reach the public npm registry. **Azure Functions Core Tools is a separate prerequisite**, not supplied by Rayfin or Foundry Dev Pack.

### Fabric Tools

Choose your tool and operating system:

| Tool | Windows | macOS |
|---|---|---|
| GitHub Copilot in VS Code | [Windows setup](../install/github-copilot-windows.md) | [macOS setup](../install/github-copilot-macos.md) |
| Cursor IDE | [Windows setup](../install/cursor-windows.md) | [macOS setup](../install/cursor-macos.md) |
| Claude Desktop chat | [Windows setup](../install/claude-desktop-windows.md) | [macOS setup](../install/claude-desktop-macos.md) |

### Foundry Tools

Install **Foundry Dev Pack** for Foundry command-line tools, the Microsoft Foundry Skill, and editor integrations. This is separate from the Fabric and Power BI skills above.

| Tool | Windows | macOS |
|---|---|---|
| Foundry Dev Pack | [Windows setup](../install/foundry-devpack-windows.md) | [macOS setup](../install/foundry-devpack-macos.md) |

[Next: Build our App](../build-app/README.md)

[Back to the hackathon](../../README.md)