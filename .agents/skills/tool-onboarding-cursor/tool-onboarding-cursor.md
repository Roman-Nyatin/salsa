# Skill: Tool Onboarding & Provisioning - Cursor

## 1. Objective
- **Purpose:** Act as an atomic pass-through transport adapter that provisions project-specific agent rules, workflows, and MCP configurations from the Single Source of Truth (`/.agents/`) into Cursor's native multi-file structure.
- **Context:** Invoked by the Meta-Agent immediately after fine-tuning or scaling framework core manifests.

## 2. Direction of Truth & File Formatting
- **Immutable Rule:** `/.agents/` remains the absolute Source of Truth (SSOT).
- **Target Subdirectories:** 
  - Rules: `/.cursor/rules/[role_name].mdc` (Requires Markdown with YAML Frontmatter).
  - Workflows: `/.cursor/commands/[role_name].md`
- **Execution Constraint:** This skill performs 1-to-1 file transport, merely wrapping rule files with the mandatory Cursor `.mdc` header format. It MUST NOT modify the core body instruction text.

## 3. Provisioning & Envelope Wrapping Steps
When synchronization is triggered for Cursor, execute these atomic operations for every active role in the matrix:

1. **Assert Containers:** Initialize and verify the physical presence of `/.cursor/rules/` and `/.cursor/commands/` folders at the workspace root.
2. **Formulate Rule Envelope (.mdc):** Read the adapted rules file from `/.agents/rules/[target_role].md`. Prepend the Cursor-native frontmatter configuration matching the role's path limits from the matrix:
   ```yaml
   ---
   description: Core operational constraints and behavioral directives for the Fast-ASDLC [Role Name] Agent.
   globs: [Insert Allowed Paths, e.g., "src/**/*, tests/**/*"]
   alwaysApply: true
   ---
   ```
3. **Publish Rules:** Write the wrapped output directly into `/.cursor/rules/[target_role].mdc`.
4. **Publish Workflows:** Copy the corresponding workflow file directly from `/.agents/workflows/[target_role].md` into `/.cursor/commands/[target_role].md` to enable explicit execution.
5. **Deploy MCP Settings:** Copy the verified master MCP configuration directly from `/.agents/mcp/mcp-settings.json` into Cursor's project-level active configuration endpoint to enforce unified tool syncing.

## 4. Operational Guardrails
- **Sync Lock:** Any removal or renaming of an agent manifest inside `/.agents/` must trigger an immediate mirror purge inside `/.cursor/rules/` and `/.cursor/commands/` to eliminate zombie rules.
- **Fail-Fast Trigger:** If the file system blocks writing to the `/.cursor/` directory tree, abort the bootstrap sequence immediately and alert the human supervisor.
