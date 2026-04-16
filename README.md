# Telerik DevTools Style Agent

This agent audits and remediates any Progress or Telerik docs-builder documentation site against the [Progress DevTools Style Guide](https://www.telerik.com/documentation/style-guide/introduction). It is product-agnostic and discovers the product name, navigation, and content layout from the repository it operates on.

## Prerequisites

- [Visual Studio Code](https://code.visualstudio.com/) with the [GitHub Copilot](https://marketplace.visualstudio.com/items?itemName=GitHub.copilot) extension installed and active.
- A Telerik or Progress documentation repository built with **docs-builder** (`docs-builder.yml`, YAML front matter).

## Installation

You can install the agent at the **workspace level** (shared with the team) or at the **user level** (personal, available across all your projects).

### Option A — Workspace-Level (Recommended for Teams)

Copy the `agents/` and `skills/` folders into the `.github/` directory of your docs repo so that Copilot discovers them automatically:

```
your-docs-repo/
├── .github/
│   ├── agents/
│   │   └── docs-style-guide.agent.md   ← from agents/
│   └── skills/
│       └── telerik-docs-style-guide/
│           └── SKILL.md                ← from skills/
```

1. Copy the `agents/` folder → `.github/agents/`
2. Copy the `skills/` folder → `.github/skills/`
3. Commit and push. Every team member with Copilot will now have access to the agent.

### Option B — User-Level (Personal)

Place the files in your Copilot user profile so the agent is available in every workspace you open:

- **Windows:** `%APPDATA%\Code\User\prompts\agents\` and `~/.copilot/skills/`
- **macOS/Linux:** `~/.config/Code/User/prompts/agents/` and `~/.copilot/skills/`

1. Copy `agents/docs-style-guide.agent.md` → `<prompts>/agents/docs-style-guide.agent.md`
2. Copy `skills/telerik-docs-style-guide/SKILL.md` → `~/.copilot/skills/telerik-docs-style-guide/SKILL.md`

## Usage

### Invoking the Agent

1. Open your docs-builder repo in VS Code.
2. Open GitHub Copilot Chat (`Ctrl+Shift+I` / `Cmd+Shift+I`).
3. Switch to **Agent mode** (click the mode dropdown at the top of the chat panel).
4. Select **docs-style-guide** from the agent picker — or type `@docs-style-guide` to address it directly.
5. Enter your request. Example prompts:

```text
Audit this docs-builder repo for Progress DevTools Style Guide compliance and fix issues by phase.
```

```text
Fix the metadata for all articles in the getting-started section.
```

```text
Check tone and voice across the entire repo.
```

### Invoking the Skill Directly

If you prefer to use the default Copilot agent with the skill loaded on demand, type `/` in chat and select **telerik-docs-style-guide** from the slash-command list.

### What Happens Next

1. The agent reads `docs-builder.yml` to discover the product, navigation tree, and articles.
2. It builds a phased plan (housekeeping → metadata → content → style → formatting) and tracks progress with a task list.
3. It processes one phase at a time, marking tasks as it goes.
4. Review the proposed changes after each phase and confirm before proceeding.

## Project Structure

| File | Purpose |
|------|---------|
| `agents/docs-style-guide.agent.md` | Full agent behavior, phased audit plan, and all style guide rules |
| `skills/telerik-docs-style-guide/SKILL.md` | Skill definition with quick-reference table of the 20 most violated rules |

## Scope and Limitations

- This agent is intended for docs-builder repositories that use docs-builder.yml.
- It does not create product content or rewrite technical requirements. It focuses on style, structure, and metadata compliance.
- It does not validate runtime behavior of code samples beyond syntax and formatting checks.
