# Cursor IDE - Windows

Choose **one complete installation option** below. Each includes **all Fabric skills**, including **`semantic-model-authoring`** and **`powerbi-report-cli`**, plus **`microsoft-foundry`**.

## 1. Install Cursor

1. Download and install [Cursor for Windows](https://cursor.com/downloads).
2. Open Cursor and sign in.
3. Open your local hackathon folder. If you have not cloned it yet, follow [First run in Cursor](#first-run-in-cursor) below.

For Node.js, Git, and other prerequisites, see [Setup Tooling](../setup/README.md#local-tools).

## 2. Install the hackathon skills

Run the commands for your chosen option from the hackathon project folder. Keep the installation project-local so Cursor can use it for this workshop.

### Option 1: Clone and copy all Fabric skills

Clone the source repositories outside Cursor's skill directory, then copy **every Fabric skill** into `.agents\skills`. Copy only `microsoft-foundry` from the Azure repository.

For a fresh setup, run:

```powershell
New-Item -ItemType Directory -Path .skill-sources, .agents\skills -Force | Out-Null
git -c core.longpaths=true clone --depth 1 https://github.com/microsoft/skills-for-fabric.git .skill-sources\skills-for-fabric
git -c core.longpaths=true clone --depth 1 https://github.com/microsoft/azure-skills.git .skill-sources\azure-skills
Copy-Item .skill-sources\skills-for-fabric\skills .agents -Recurse -Force
Copy-Item .skill-sources\skills-for-fabric\common .agents -Recurse -Force
Copy-Item .skill-sources\skills-for-fabric\mcp-setup .agents -Recurse -Force
Copy-Item .skill-sources\azure-skills\skills\microsoft-foundry .agents\skills -Recurse -Force
```

The skills now sit directly in folders such as `.agents\skills\powerbi-report-cli` and `.agents\skills\microsoft-foundry`, rather than inside nested repository folders. Keep `.agents\common` and `.agents\mcp-setup`: Fabric skills reference these shared files and setup guidance. Copying them does not configure MCP connections. The source clones and installed content are ignored by this hackathon's `.gitignore`.

In Cursor's Skills view, look for **`powerbi-report-cli`** for report authoring. **`powerbi-authoring`** is a marketplace plugin name, not an individual skill.

### Option 2: APM backup

Install **APM (Agent Package Manager)** if it is missing:

```powershell
irm https://aka.ms/apm-windows | iex
```

Restart your terminal and Cursor after installation. If `apm` is not recognized, open a new PowerShell terminal so it picks up the updated PATH.

From the hackathon folder, run both commands:

```powershell
apm install microsoft/skills-for-fabric --target cursor --only apm
apm install microsoft/azure-skills --skill microsoft-foundry --target cursor --only apm
```

APM installs the Fabric/Power BI collection and the Foundry skill, preserving and rewriting shared references. Keep `apm_modules` in the project: installed skills use it. `--only apm` skips MCP server registration.

After your chosen installation, restart Cursor and reopen the hackathon folder. These options install skill files, not local development tools, authentication, or permissions. Continue with [Foundry Tools](../setup/README.md#foundry-tools) for the separate Foundry tooling setup.

## First run in Cursor

### Clone and open the hackathon repository

This clones the **hackathon repository**, not the skill repositories in option 1 above. Do this before running the skill installation commands if you do not already have the hackathon on your computer.

1. Press **Ctrl+Shift+P** and search for **Git: Clone** or **Clone Repository**.
2. Paste the hackathon repository URL provided by the organizer and choose a local directory.
3. Open the cloned folder in Cursor and select that repository when starting a conversation.

![Cursor command search showing Clone Repository.](../images/cursor-clone-repository.png)

If the repository appears in the sidebar but you do not see a file tree, ask your agent to open `README.md`. The agent can work with the files in the selected repository even when the sidebar is showing conversations rather than Explorer.

![Cursor conversation with the cloned hackathon README open beside it.](../images/cursor-cloned-repository-readme.png)

### Run your first local-tools check

Open [Setup Tooling's local-tools prompt](../setup/README.md#check-your-local-tools-with-your-coding-agent), copy it, and paste it into a chat for the cloned hackathon repository. Allow the version and package-access checks when Cursor asks.

The agent should report which tools are installed, missing, or incompatible, with next actions. The prompt does not install anything or change settings. Complete any missing local-tool setup before running the skill installation commands above; this check is separate from Fabric and Foundry access.

### If npm access is blocked

Use your organization's approved npm registry. **For Microsoft-managed devices only**, if your IT documentation directs you to the Microsoft package proxy, open Cursor's PowerShell terminal and run:

```powershell
npm config set registry https://packagefeedproxy.microsoft.io/npm/ --location=user
npm view @microsoft/create-rayfin version
```

This changes your user-level npm registry across projects. Other participants should use their own approved registry, not assume access to Microsoft's proxy. A package lookup is more useful here than `npm ping`, which can return 404 on this proxy. Rerun the local-tools prompt after resolving the registry issue.

References: [Cursor skill directories](https://cursor.com/docs/skills#skill-directories), [Microsoft Fabric skills](https://github.com/microsoft/skills-for-fabric), and [Microsoft Azure skills](https://github.com/microsoft/azure-skills).

[Back to installation guides](README.md) | [Back to Setup Tooling](../setup/README.md)

[Back to the hackathon](../../README.md)
