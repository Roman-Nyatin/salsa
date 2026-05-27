# Workflow: QA Agent - Generate Test Suite

## 1. Objective & Scope
- **Purpose:** Automate the transition from analytical requirements to a concrete, executable automated test framework.
- **Scope:** Runs during Phase 4 (Validation) within a dedicated feature branch. Authorized to write only to the `/tests/` directory and append metadata to the active `.backlog/` task tracker file.

## 2. Triggering Conditions & Inputs
- **Trigger:** A build readiness notification or task activation marker appended to the active `.backlog/` feature file by the human manager or upstream agents.
- **Inputs:**
  - Analytical blueprints located in `/docs/domain/usecases/` containing explicit Acceptance Criteria.
  - Complete technical specifications and contract declarations found in `/docs/specs/`.
  - The project configuration state declared in `/.agents/memory-bank/project-brief.md` (Tech Stack, Testing Framework, Language Policy).

## 3. Step-by-Step Execution Lifecycle

### Phase 1: Context Assembly & Matching
1. **Analyze Contracts:** Ingest the active feature specifications from `/docs/specs/`. Extract class names, method signatures, REST endpoints, and queue payloads.
2. **Ingest Criteria:** Parse the corresponding Use Cases in `/docs/domain/usecases/`. Isolate the scenario flows and formal Acceptance Criteria definitions.
3. **Map Framework Syntax:** Read the targeted test framework, runtime stack, and localization guidelines from the project brief (e.g., PyTest for Python, JUnit for Java, Playwright for Node.js).

### Phase 2: Test Suite Design (Plan Mode)
4. **Draft Test Cases:** Formulate a structured markdown draft enumerating the exact integration, component-level, and regression test cases required to validate every boundary path.
5. **Establish Language Bounds:** Apply the language parameters from the project brief to ensure all test case naming structures, assertions, and test data match company standards.
6. **Role Isolation Check:** Verify that no code scripts target internal private domains. Test setups must exclusively access ports and adapters following the hexagonal schema.

### Phase 3: Quality Gate 1 (Human Scenario Approval)
7. **Present Draft:** Present the structured test case list and scenario mapping blocks directly to the human supervisor in the chat interface.
8. **Await Human Sign-Off:** Pause execution. Wait for formal human validation. If the human rejects or modifies the coverage plan, loop back to Step 4.

### Phase 4: Test Scaffolding & Code Generation (Act Mode)
9. **Scaffold Files:** Initialize or append code assets inside the appropriate subfolders under the `/tests/` partition.
10. **Write Automated Tests:** Generate clean, production-grade, unpolluted automated test code matching the approved scenarios. Ensure zero dependencies on external live infrastructure by preparing targets for environment stubbing.
11. **Anti-Redundancy Sanity Check:** Ensure the suite contains no duplicated boilerplate, maintains an imperative style, and omits inline meta-explanations.

### Phase 5: Pipeline Synchronization & Handoff
12. **Register Suite:** Append the file paths of all newly created or updated test assets to the active `.backlog/` tracking file.
13. **Progress Transition:** Update `/.agents/memory-bank/active-context.md` to flag the feature as structurally ready for execution, and signal the next automation sequence (`/.agents/workflows/qa-execute-dynamic-testing.md`).
