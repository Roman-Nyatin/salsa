# Workflow: QA Agent - Execute Non-Functional Testing

## 1. Objective & Scope
- **Purpose:** Orchestrate and execute automated performance (load/stress) profiles and Application Security (AppSec SAST/DAST) scanning via native IDE terminal utilities, ensuring zero systemic regression or vulnerability leakage.
- **Scope:** Runs during Phase 4 (Validation) inside the active feature branch, strictly after all functional tests pass. Authorized to write output telemetry and vulnerability logs to `.backlog/` and wipe temporary diagnostic binaries. Restricted from mutating `/src/` or `/docs/`.

## 2. Triggering Conditions & Inputs
- **Trigger:** Successful validation sign-off from the `qa-execute-dynamic-testing.md` workflow (100% functional pass and target coverage barriers validated).
- **Inputs:**
  - Environmental deployment manifests located in `/infra/`.
  - Upstream Threat Models and Security Risk Assessments built inside `/docs/architecture/` or `/docs/security/`.
  - Target load profiling limits and threshold metrics defined in the local configuration memory.

## 3. Step-by-Step Execution Lifecycle

### Phase 1: Performance Profiling & Load Testing
1. **Boot Sandbox SUT:** Execute the targeted deployment scripts inside `/infra/` via the native terminal to stand up an isolated release build of the System Under Test (SUT).
2. **Inject Performance Profiler:** Invoke the project-specific technical loading capabilities and performance execution configurations provisioned for this runtime profile, following the exact rules inside: `[Path to Specific Performance Testing Skill]`.
3. **Run Performance Assertions:** Execute load tests (e.g., spike, stress, endurance) to capture telemetry (latency percentiles, error rates, CPU/memory leakage). Assert that performance budgets match the thresholds mapped in the project specifications.

### Phase 2: Automated Security Analysis (AppSec / Shift-Left Security)
4. **Trigger Static Scan (SAST):** Run non-interactive static analysis wrappers over the codebase inside `/src/` using the precise tool arguments defined inside: `[Path to Specific Security Scanning Skill]`. Inspect for hardcoded keys, injection vulnerabilities, and flawed algorithmic dependencies.
5. **Trigger Dynamic Scan (DAST):** Attack the running sandbox SUT using container vulnerability interceptors to parse API exposures against top compliance hazards (e.g., OWASP Top 10).
6. **Cross-Reference Threat Model:** Correlate detected exposures against the Threat Model artifacts established in Phase 1 to calculate explicit risk impacts.

### Phase 3: Defect Isolation & Backtrack Gating
7. **Generate Non-Functional Failure Report:** If any load test violates performance thresholds (e.g., error rates >0.1% or p95 latency spikes) or any AppSec scanner yields unresolved security vulnerabilities, halt the deployment path. Log an explicit defect trace inside the active `.backlog/` feature file detailing:
   - Specific performance bottleneck metrics or code/infrastructure vulnerability CVE indicators.
   - Remediation action items mapped precisely for the Programmer Agent or DevOps engineers.
8. **Signal Backtrack Loop:** Route execution parameters back to the Programmer Agent in the chat, shift the state to a blocked signal in `/.agents/memory-bank/active-context.md`, and pause until a new bugfix iteration is declared.

### Phase 4: Quality Gate (Human Audit & Sign-Off)
9. **Compile Compliance Report:** Once performance budgets are satisfied and all AppSec barriers return clean, zero-vulnerability states, compile the raw execution reports and security sign-off manifests.
10. **Await Human Audit:** Pause execution. Present the verified load telemetry charts, performance budget scorecards, and clean AppSec security compliance traces to the human supervisor for formal verification sign-off.

### Phase 5: Decommission & Framework Release
11. **Tear Down Production Environment:** Terminate all active container sandboxes and clean up transient performance metric caches via the native IDE terminal interface.
12. **Authorize Core Delivery:** Update `/.agents/memory-bank/progress.md` and `/.agents/memory-bank/decision-log.md`. Toggle `/.agents/memory-bank/active-context.md` to flag the feature branch as fully validated and safe for final production branch merging via Phase 5 pipelines.
