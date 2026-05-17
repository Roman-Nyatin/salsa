# Skill: Tool Onboarding & Provisioning - Cline

## 1. Objective
- **Purpose:** Act as a pass-through transport adapter that provisions customized agent rules, workflows, and MCP configurations from the Single Source of Truth (`/.agents/`) into the native Cline runtime environment.
- **Context:** Invoked by the Meta-Agent immediately after completing any agent adaptation, tooling update, or MCP infrastructure tuning.

## 2. Direction of Truth & Write Boundaries
- **Immutable Rule:** `/.agents/` is the absolute Source of Truth (SSOT). Files inside this folder already contain all project-specific adaptations completed by the Meta-Agent.
- **Source Paths:** 
  - Rules: `/.agents/rules/[target_role].md`
  - Workflows: `/.agents/workflows/[target_role].md`
  - MCP Config: `/.agents/mcp/mcp-settings.json`
- **Target Runtime Environment:** `/.clinerules/` (for roles), `/.clinerules/workflows/` (for sequences), and the tool's expected active `mcp-settings.json` file.
- **Execution Constraint:** This skill performs raw 1-to-1 file system transport. It MUST NOT modify, append, or transform text during execution.

## 3. Provisioning Execution Steps
When a synchronization or initial bootstrap is triggered for Cline, execute these atomic operations:

1. **Assert Environment:** Verify the physical presence of the `/.clinerules/workflows/` folder structure at the root. Create if missing.
2. **Deploy Active Rules:** Perform a direct, unmutated copy of the tailored rule file from `/.agents/rules/[target_role].md` over to `/.clinerules/[target_role].md`.
3. **Deploy Active Workflows:** Perform a direct, unmutated copy of the workflow file from `/.agents/workflows/[target_role].md` over to `/.clinerules/workflows/[target_role].md`.
4. **Deploy MCP Settings:** Copy the verified master MCP configuration directly from `/.agents/mcp/mcp-settings.json` into the target environment's active `mcp-settings.json` file to align low-level tool access with the project matrix.
5. **Mirror State:** Ensure that any deletion or renaming of an asset in `/.agents/` triggers an immediate mirror deletion in `/.clinerules/` to prevent ghost rules.
