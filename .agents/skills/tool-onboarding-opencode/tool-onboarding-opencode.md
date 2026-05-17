# Skill: Tool Onboarding & Provisioning - OpenCode

## 1. Objective
- **Purpose:** Act as a pass-through transport adapter that provisions fully configured on-premise enterprise agent configurations and MCP tool connections from the Single Source of Truth (`/.agents/`) into the secure native OpenCode runtime environment.
- **Context:** Invoked by the Meta-Agent immediately after fine-tuning or scaling the framework's enterprise workforce.

## 2. Direction of Truth
- **Immutable Rule:** Every asset in `/.agents/` is fully hydrated with corporate tech stack standards, enterprise security compliance parameters, and secure on-premise MCP tool definitions before this skill executes.
- **Source Paths:**
  - Rules: `/.agents/rules/[target_role].md`
  - Workflows: `/.agents/workflows/[target_role].md`
  - MCP Config: `/.agents/mcp/mcp-settings.json`
- **Target Location:** Root-level secure container `/.clinerules/`, `/.clinerules/workflows/`, and the enterprise `mcp-settings.json` sandbox location.

## 3. Provisioning Execution Steps
1. **Assert Container:** Ensure the local folder structure for `/.clinerules/workflows/` is initialized.
2. **Deploy Enterprise Rules:** Copy the fully adapted rule architecture from `/.agents/rules/[target_role].md` directly to `/.clinerules/[target_role].md` without text transformations.
3. **Deploy Enterprise Workflows:** Copy the execution sequence manifest from `/.agents/workflows/[target_role].md` directly to `/.clinerules/workflows/[target_role].md`.
4. **Deploy On-Prem MCP:** Copy the locked corporate MCP tool configuration from `/.agents/mcp/mcp-settings.json` straight into OpenCode's designated active `mcp-settings.json` file.
5. **Atomic Sync Verification:** If a file transport error occurs, halt the pipeline immediately to prevent partial runtime deployment or security gate leakage.
