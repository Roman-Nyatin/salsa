# Development Setup

This guide helps new team members configure their local environment for working with SALSA.

## Quick Start (5 minutes)

### 1. Install OpenCode

- Install **VS Code** if not already installed
- Install **OpenCode extension** for VS Code
- Configure **OpenRouter API key** in OpenCode settings

### 2. AI Models Configuration

When you open this project in OpenCode, the workspace will automatically use the models defined in `opencode.json`:

| Mode | Model | Purpose |
|------|-------|---------|
| **Plan** | `kimi-k2.5` | Analysis, architecture, reasoning |
| **Build** | `minimax-m2.1` | Code generation, refactoring |

### 3. Verify Setup

1. Open any file in the project
2. Switch to **Build Mode** (Cmd/Ctrl + Shift + P → "OpenCode: Switch Agent Mode" → "Build")
3. Ask: "What model are you?"
4. Verify response mentions Minimax or minimax-m2.1

---

## Model Selection Rationale

### Why Kimi k2.5 for Plan Mode?

- Strong reasoning capabilities for architecture and design
- Optimized for structured output (Markdown, Mermaid diagrams)
- Handles long context well (important for C4 models)

### Why Minimax M2.1 for Build Mode?

- Specialized in code generation
- Faster and more cost-effective for routine coding tasks
- Better at generating tests and boilerplate code

**Decision date:** 2026-06-28

See: [.agents/memory-bank/decision-log.md](.agents/memory-bank/decision-log.md) for full context.

---

## AI Agent Configuration

### Unified Structure: OpenCode + Cline

Both OpenCode and Cline use the same files from `/.clinerules/`:

| Mode | Rules File | Workflow File | Model |
|------|------------|---------------|-------|
| Plan | `/.clinerules/plan.md` | `/.clinerules/workflows/plan.md` | Kimi k2.5 |
| Build | `/.clinerules/build.md` | `/.clinerules/workflows/build.md` | Minimax M2.1 |

**How it works:**

- OpenCode reads from `/.clinerules/` via `opencode.json`
- Cline reads from `/.clinerules/` natively (as expected)
- Files contain reduced rules with links to canonical sources

### Canonical Sources (Source of Truth)

For other roles (analyst, architect, programmer, qa):

- `/.agents/rules/[role].md` — full rules
- `/.agents/workflows/[role].md` — full workflows

---

## MCP Filesystem Server Setup

MCP (Model Context Protocol) server is configured in `opencode.json` and provides safe filesystem access for the Build agent.

### Configuration

MCP servers are defined in the `mcpServers` section of `opencode.json`:

```json
{
  "mcpServers": {
    "filesystem": {
      "type": "stdio",
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-filesystem",
        "./"
      ]
    }
  }
}
```

### Installation

Install the MCP filesystem server globally:

```bash
npm install -g @modelcontextprotocol/server-filesystem
```

### Safety Rules

Safety rules are defined in Build agent instructions (`/.clinerules/build.md`):

| Operation | Allowed Paths | Confirmation Required |
|-----------|---------------|----------------------|
| **Read** | Any file | No |
| **Write** | `/src/`, `/tests/`, `/infra/`, `/.backlog/` | No |
| **Delete** | `/src/`, `/tests/` | No |
| **Delete** | `/.agents/`, `/.clinerules/`, `/docs/`, `/infra/` | **Yes** |
| **Forbidden** | `/.agents/memory-bank/`, `/.clinerules.backup` | N/A |

### Verification

After restarting VS Code:

1. Open OpenCode panel
2. Switch to **Build Mode**
3. Verify model shows **Minimax M2.1**
4. Verify MCP tools appear in the tool list
5. Try creating a test file: "Create a test file at `/src/test-mcp.txt`"

### Troubleshooting MCP

#### "MCP server not found"

1. Verify installation: `npm list -g @modelcontextprotocol/server-filesystem`
2. Check npx availability: `which npx`
3. Restart VS Code completely

#### MCP tools not appearing

1. Check `opencode.json` contains `mcpServers` section
2. Verify JSON is valid
3. Restart VS Code

#### Model doesn't change to Minimax in Build Mode

1. Check `opencode.json` has correct model for build agent
2. Restart VS Code completely (not just reload window)
3. Check OpenCode version supports per-mode models
- Use Plan mode for operations outside `/src/`, `/tests/`, `/infra/`, `/.backlog/`
- Critical directories (memory-bank, backups) are protected

#### MCP tools not appearing

1. Check `opencode.json` contains `"mcp": { "configPath": "./mcp-config.json" }`
2. Verify `mcp-config.json` exists at project root
3. Restart VS Code

---

## Troubleshooting

### Model doesn't change when switching modes

1. Check that `opencode.json` exists at project root
2. Restart VS Code / OpenCode
3. If still not working, select model manually in OpenCode UI

### OpenCode doesn't see the project config

Ensure you're opening the project folder (`/salsa`) directly in VS Code, not a subfolder.

---

## Additional Resources

- [CONTRIBUTING.md](CONTRIBUTING.md) — Contribution process
- [AGENTS.md](AGENTS.md) — AI agent rules
- [.agents/memory-bank/](.agents/memory-bank/) — Project context and decisions
