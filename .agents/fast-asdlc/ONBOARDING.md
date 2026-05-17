# Fast-ASDLC Onboarding Playbook

Welcome to your AI-native software engineering environment. This playbook outlines the step-by-step procedure to transition this repository from an abstract template into a production-ready, agentic software factory customized for your product.

---

## 🔁 The Architecture of Onboarding
1. **The Human** triggers the `BOOTSTRAP-PROMPT.md`.
2. **The Meta-Agent** initializes, interviews the human, and populates the localized Memory Bank.
3. **The Meta-Agent** provisions custom agent profiles and generates environment dotfiles (`.cursorrules`, `.clinerules`, `mcp-settings.json`).
4. **The Project Agents** spin up inside their restricted sandboxes, ready to pull tasks from `.backlog/`.

---

## 🛠 Step-by-Step Bootstrap Protocol

### Step 1: Initialize the Meta-Agent Interface
1. Open this cloned repository inside your target AI orchestration interface (e.g., **Cursor**, **VS Code with Cline**, **Windsurf**, or a custom **CLI wrapper**).
2. Open the AI Chat sidebar.
3. Copy the **entire content** of `/.agents/fast-asdlc/BOOTSTRAP-PROMPT.md` and paste it directly into the chat.
4. The assistant will dynamically absorb its instructions from `/.agents/rules/meta-agent.md` and enter **Plan Mode**.

### Step 2: The Project Discovery Interview
1. The Meta-Agent will ask you a series of dense, technical questions. Prepare to provide:
   - Your primary product vision and target contexts.
   - Your exact technology stack (Backend ecosystem, Frontend framework, Database engines).
   - Your preferred **Language & Documentation Policy** (e.g., Russian for analytics, English for codebase comments).
   - Your local AI execution stack (Inference platform like Ollama/vLLM, and specific models like Qwen/GLM).
2. Answer the agent directly in the chat. The agent will aggregate your answers and draft the system memory.

### Step 3: Hydrate the Local Memory Bank
1. Once conceptual consensus is achieved, the Meta-Agent will write the structural specifications to:
   - `/.agents/memory-bank/project-brief.md`
   - `/.agents/memory-bank/process-overview.md`
2. Review these files locally. Commit them to your current working feature branch.

### Step 4: Workforce & IDE Provisioning
1. The Meta-Agent will execute `/.agents/workflows/meta-agent-bootstrap-workforce.md`.
2. It will automatically generate or update the core pipeline manifests:
   - `analyst.md`, `architect.md`, `programmer.md`, and `qa.md` inside `/.agents/rules/` and `/.agents/workflows/`.
3. The Meta-Agent will automatically compile configuration mappings to bridge the gap with your IDE:
   - **Cursor/Windsurf:** Populates the root level `.cursorrules` file.
   - **Cline/OpenCode:** Populates the root level `.clinerules` file.

### Step 5: Bridge Tools via MCP
1. If your tech stack or process overview requires deeper system access (e.g., direct DB inspection, file system access, or tracking task statuses in Jira), the Meta-Agent will calculate the necessary integrations.
2. It will generate or append instructions to your local `mcp-settings.json` profile. 
3. Restart your IDE or inference tool extension to apply the active MCP servers.

---

## 🏁 Verification & Next Steps
Your agentic infrastructure is fully onboarded when the Meta-Agent declares system readiness and updates `/.agents/memory-bank/active-context.md`.

To begin actual product development:
1. Navigate to `.backlog/README.md` to see how to structure your tracking elements.
2. Create your first production item in `.backlog/` (e.g., `004-initialize-core-auth.md`).
3. Pass that intention file to your newly configured **Analyst Agent** to kick off the spec-driven AI-native agentic SDLC pipeline.
