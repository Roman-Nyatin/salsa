# Workflow: Meta-Agent - Bootstrap Workforce

## 1. Objective & Scope
- **Purpose:** Guide the human through project discovery, populate the local Memory Bank, and generate customized tool/agent configurations mapped to specific IDEs and workspaces.
- **Scope:** Runs exclusively in Post-Clone mode. Authorized to write to `/.agents/`, root dotfiles (`.cursorrules`, `.clinerules`), and directory-specific configs.

## 2. Triggering Conditions
- Executed immediately when the human injects the `BOOTSTRAP-PROMPT.md` payload into the AI chat interface.

## 3. Step-by-Step Execution Lifecycle

### Phase 1: Interactive Project Discovery (Plan Mode)
1. **Initiate Interview:** Present the human with a structured questionnaire covering the product vision, language policy, tech stack, local LLM runtime specs, and the **Role-to-Tool Matrix**.
2. **Collect Intent:** Process human replies incrementally. Update internal context configuration state.
3. **Draft Memory Bank:** Generate the complete markdown structures for `/.agents/memory-bank/project-brief.md` and `/.agents/memory-bank/process-overview.md`.

### Phase 2: Quality Gate 1 (Human Verification of Context)
4. **Present Manifest Drafts:** Display the completed Brief and Overview markdown drafts (including the mapped IDE matrix) to the human.
5. **Acknowledge Sign-off:** Wait for the human to confirm the parameters are correct. If approved, write files to disk and proceed to Phase 3.

### Phase 3: Workforce Customization (Act Mode)
6. **Generate Role Manifests:** Generate or overwrite downstream agent definitions based on tech stack and Language Policy:
   - `/.agents/rules/analyst.md` & `/.agents/workflows/analyst.md`
   - `/.agents/rules/architect.md` & `/.agents/workflows/architect.md`
   - `/.agents/rules/programmer.md` & `/.agents/workflows/programmer.md`
   - `/.agents/rules/qa.md` & `/.agents/workflows/qa.md`
7. **Inject Skills & Constraints:** Map required programming skills and language restrictions into each generated agent profile.

### Phase 4: Multi-IDE Tooling Provisioning
8. **Analyze Matrix:** Parse Section 2.1 of `process-overview.md` to identify target IDEs and their respective Workspace Restrictions.
9. **Scaffold Cursor Environments:** If an agent uses Cursor, invoke the specific capability in `/.agents/skills/tool-onboarding-cursor/tool-onboarding-cursor.md` to compile identities and directory restrictions into the root `.cursorrules`.
10. **Scaffold Cline/OpenCode Environments:** If an agent uses Cline or OpenCode, invoke the corresponding capability in `/.agents/skills/tool-onboarding-cline/tool-onboarding-cline.md` or `/.agents/skills/tool-onboarding-opencode/tool-onboarding-opencode.md` to generate scoped rulesets.
11. **Configure MCP settings:** Write or append paths to `mcp-settings.json` for tool enablement (File system permissions mapped precisely to role restrictions).
12. **Finalize Setup:** Log initialization in `/.agents/memory-bank/decision-log.md` and instruct the user on how to pass the first task to the Analyst Agent.

