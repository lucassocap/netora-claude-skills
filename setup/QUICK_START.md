# Quick Start Guide

Set up Claude as your Netora AI assistant in 5 minutes.

## Prerequisites

- [ ] Netora Upstream Platform account
- [ ] Claude.ai Pro or Team subscription
- [ ] Your Netora API key

## Step 1 — Get Your API Key

1. Log in to the Netora Upstream Platform
2. Go to **Settings > API Keys**
3. Click **Create New Key**
4. Copy the key — you'll need it in Step 2

> **Security:** Your API key has full access to your projects. Never share it publicly.

## Step 2 — Add MCP Integration in Claude.ai

1. Open [claude.ai](https://claude.ai) and log in
2. Click the **gear icon** (Settings) in the bottom-left
3. Go to **Integrations** (or **Features > MCP**)
4. Click **Add Integration**
5. Fill in:

| Field | Value |
|-------|-------|
| **Integration name** | `Netora Upstream` |
| **Server URL** | `https://api-production-fa50.up.railway.app/api/ai/tools/mcp/` |
| **Authentication type** | Bearer Token |
| **Token** | Paste your API key from Step 1 |

6. Click **Save**
7. You should see a green checkmark indicating the connection is active

## Step 3 — Create a Claude Project

1. In Claude.ai, click **Projects** in the sidebar
2. Click **New Project**
3. Name it (e.g., "Netora E&P Analysis")
4. In the **System Prompt** field, paste the entire contents of:
   - English: [`system-prompt/netora-system-prompt.md`](../system-prompt/netora-system-prompt.md)
   - Spanish: [`system-prompt/netora-system-prompt-es.md`](../system-prompt/netora-system-prompt-es.md)

## Step 4 — Upload Knowledge Files

1. In your project, go to **Project Knowledge**
2. Upload all 6 files from the [`knowledge/`](../knowledge/) folder:
   - `01-tool-catalog.md`
   - `02-domain-glossary.md`
   - `03-workflow-reference.md`
   - `04-fiscal-regimes.md`
   - `05-report-catalog.md`
   - `06-data-model.md`

> These files give Claude deep context about the platform's tools, petroleum engineering terminology, and available workflows.

## Step 5 — Test the Connection

Open a new chat in your project and type:

```
List all my projects.
```

Claude should call the `list_projects` tool and show your Netora projects.

### More Test Prompts

```
Show me the details of my first project including all fields and wells.
```

```
What are the economics assumptions for project "Permian Basin Dev"?
```

```
Run a DCA forecast for well TJ-001 and tell me the EUR.
```

## What's Next?

- Browse the [Skills Library](../skills/) for ready-to-use prompts
- Check the [Examples](../examples/) for complete walkthroughs
- See [Troubleshooting](TROUBLESHOOTING.md) if something doesn't work

## Tips for Best Results

1. **Be specific with project/well names** — Claude will search for them using the exact text you provide
2. **State your assumptions** — "Use $70/bbl oil price and 10% discount rate"
3. **Ask for units** — Claude will include units by default, but you can ask for specific ones
4. **Request sensitivity analysis** — "Run economics and show me the tornado chart"
5. **Use the skills** — Copy-paste from the `skills/` folder for pre-built analysis workflows
