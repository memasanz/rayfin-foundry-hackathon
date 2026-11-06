# Welcome to the Rayfin & Foundry Hackathon

## Overview

1. [Setup Tooling](#setup-tooling)
2. [Build our App](#build-our-app)
3. [Update our App](#update-our-app)
4. [Build a Foundry Agent](#build-a-foundry-agent)

## Setup Tooling

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
| go-sqlcmd | Optional; current Go variant | Validate queries against the lakehouse SQL analytics endpoint | [sqlcmd](https://learn.microsoft.com/sql/tools/sqlcmd/sqlcmd-download-install) | `sqlcmd --version` |
| Playwright with Chromium | Optional; project-local | Browser checks of the deployed app | [Playwright](https://playwright.dev/docs/intro) and [browsers](https://playwright.dev/docs/browsers#install-browsers) | `npx playwright --version` |

On macOS, use `python3 --version` if `python` is unavailable. For Playwright, follow the scaffolded project's dependencies and browser-installation instructions rather than initializing another project; its version check does not confirm Chromium is installed.

Rayfin is fetched through `npx` and `npm create`; no global Rayfin installation is needed. Your npm must be able to reach the public npm registry. **Azure Functions Core Tools is a separate prerequisite**, not supplied by Rayfin or Foundry Dev Pack.

### Fabric Tools

Choose your tool and operating system:

| Tool | Windows | macOS |
|---|---|---|
| GitHub Copilot in VS Code | [Windows setup](docs/install/github-copilot-windows.md) | [macOS setup](docs/install/github-copilot-macos.md) |
| Cursor IDE | [Windows setup](docs/install/cursor-windows.md) | [macOS setup](docs/install/cursor-macos.md) |
| Claude Desktop chat | [Windows setup](docs/install/claude-desktop-windows.md) | [macOS setup](docs/install/claude-desktop-macos.md) |

### Foundry Tools

Install **Foundry Dev Pack** for Foundry command-line tools, the Microsoft Foundry Skill, and editor integrations. This is separate from the Fabric and Power BI skills above.

| Tool | Windows | macOS |
|---|---|---|
| Foundry Dev Pack | [Windows setup](docs/install/foundry-devpack-windows.md) | [macOS setup](docs/install/foundry-devpack-macos.md) |

## Let's get started

Complete the tooling setup above, then work through the stages below. These are exercise outlines. Detailed instructions will be added next.

## Build our App

1. [Create a semantic model in Fabric](docs/getting-started/01-semantic-model/README.md)
2. [Build a visualization](docs/getting-started/02-build-visualization/README.md)

## Update our App

1. [Change the visualization](docs/getting-started/03-change-visualization/README.md)
2. [Create a writeback](docs/getting-started/04-writeback/README.md)

## Build a Foundry Agent

Build a Foundry agent. Detailed instructions will be added here.