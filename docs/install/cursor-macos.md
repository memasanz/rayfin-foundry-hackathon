# Cursor IDE - macOS

Choose **one complete installation option** below. Each includes Fabric skills, **Power BI authoring** (`semantic-model-authoring` and `powerbi-report-cli`), and **`microsoft-foundry`**.

## 1. Install Cursor

1. Download and install [Cursor for macOS](https://cursor.com/downloads).
2. Open Cursor and sign in.
3. Open your local hackathon folder.

For Node.js, Git, and other prerequisites, see [Setup Tooling](../setup/README.md#local-tools).

## 2. Install the hackathon skills

Run the commands for your chosen option from the hackathon project folder. Keep the installation project-local so Cursor can use it for this workshop.

### Option 1: Clone both repositories

Clone the full repositories under `.agents/skills`:

```bash
mkdir -p .agents/skills
git clone https://github.com/microsoft/skills-for-fabric.git .agents/skills/skills-for-fabric
git clone https://github.com/microsoft/azure-skills.git .agents/skills/azure-skills
```

Cursor supports nested skill folders under `.agents/skills`. Keeping each repository intact preserves its references and supporting files. The Fabric repository includes Power BI authoring; the Azure repository includes `microsoft-foundry` and additional Azure skills.

### Option 2: APM backup

Install **APM (Agent Package Manager)** if it is missing:

```bash
curl -sSL https://aka.ms/apm-unix | sh
```

Restart your terminal and Cursor after installation. If `apm` is not found, open a new Terminal window so it picks up the updated PATH.

From the hackathon folder, run both commands:

```bash
apm install microsoft/skills-for-fabric --target cursor --only apm
apm install microsoft/azure-skills --skill microsoft-foundry --target cursor --only apm
```

APM installs the Fabric/Power BI collection and the Foundry skill, preserving and rewriting shared references. Keep `apm_modules` in the project: installed skills use it. `--only apm` skips MCP server registration.

After your chosen installation, restart Cursor and reopen the hackathon folder. These options install skill files, not local development tools, authentication, or permissions. Continue with [Foundry Tools](../setup/README.md#foundry-tools) for the separate Foundry tooling setup.

References: [Cursor skill directories](https://cursor.com/docs/skills#skill-directories), [Microsoft Fabric skills](https://github.com/microsoft/skills-for-fabric), and [Microsoft Azure skills](https://github.com/microsoft/azure-skills).

[Back to installation guides](README.md) | [Back to Setup Tooling](../setup/README.md)

[Back to the hackathon](../../README.md)
