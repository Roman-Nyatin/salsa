# Fast-ASDLC Onboarding Interview: SALSA
## Draft answers derived from `docs/domain/safe-agentic-operating-system-proposal.md`

## 1. Core Product
- **Final product name:** SALSA (Scaled Agentic Lean Secure Agile) — open-source implementation core of the broader **SAFe Agentic Operating System (SAFe AOS)** concept.
- **One-liner vision:** A **Framework-as-Code** extension to SAFe 6.0 that transforms the methodology from static documentation into an active, AI-native operating system, with Git (Markdown + Mermaid.js) as the single source of truth.
- **Target audience:**
  - Enterprise C-level / Portfolio leadership
  - Lean Portfolio Management (LPM), Epic Owners
  - Release Train Engineers (RTE), Product Management, System Architects
  - Agile teams, SPCs, DevSecOps, SRE, AppSec engineers
- **Key success metric:** Radical reduction of Time-to-Market by **60–80%**, elimination of hand-off delays, automated backlog readiness, built-in quality, lean overhead reduction.
- **MVP scope (from proposal):**
  - Open Source Core: Meta-agent prompts, role-specific skill library, Mermaid.js visualization templates for Portfolio & Solution Intent.
  - End-to-end Private Demo: One hypothetical Epic flowing from Lean Business Case (MD) through AI-Native SDLC to automated release.
- **Explicit non-scope (inferred):**
  - Not a replacement for SAFe; positioned as a toolkit for SPCs that complements the methodology.
  - Full enterprise UI/dashboard layer is an aspiration (mentioned for C-level), not necessarily part of MVP.

## 2. Language & Documentation Policy
- **Agent system prompts / rules / workflows / skills:** English-only everywhere.
- **Project documentation:** English-only everywhere.
- **Recommended policy (requires confirmation):** English-only for all system artifacts; Russian permitted only in legacy/transitional business proposals or external presentations, not in code/docs/backlog.
- **Source code comments, logs, error messages:** English-only everywhere.
- **Git commit messages:** English, Conventional Commits.
- **Backlog / task tracker entries:** English and Russian.

## 3. Technical Stack
- **Backend language & framework:** TBD
- **Frontend framework:** TBD
- **Primary database engine:** TBD
- **Message broker / event streaming:** TBD
- **API style:** TBD
- **Monorepo / multi-repo:** Current repo is monorepo; keep it.
- **Package manager & build tool:** TBD

## 4. AI Runtime Environment
- **Deployment strategy:** Local-LLM first, within a secure corporate perimeter / protected contour.
- **Inference engine:** TBD
- **Primary reasoning / orchestration model:** TBD

## 5. Human-Agent Interface & Role-to-Tool Matrix
- All roles work in OpenCode

- **Additional proposal roles to consider as separate manifests:**
  - Epic Owner Agent
  - Lean Portfolio Management (LPM) Agent
  - Release Train Engineer (RTE) Agent
  - Product Management Agent
  - System Architect Agent
  - Tech Lead Agent
  - SRE Agent
  - AppSec / Cybersecurity Agent

- **Primary IDE environment for the team:** VSCode + opencode

## 6. Infrastructure & DevSecOps
- **Local dev sandbox engine:** TBD
- **Target cloud / runtime:** TBD
- **CI/CD orchestration tool:** TBD
- **Infrastructure-as-Code engine:** TBD
- **Application security tooling:** TBD
- **Container registry / artifact store:** TBD

## 7. Domain Boundaries (DDD Bounded Contexts for SALSA)
Derived from proposal:

1. **Portfolio Management** — Strategic themes, investment horizons, Lean Business Case, WSJF, Epic Owner workflow.
2. **Lean Portfolio Orchestration** — LPM monitoring, budget guardrails, compliance alignment.
3. **ART / Program Coordination** — PI Planning, Program Board (Mermaid.js), dependencies, RTE workflow.
4. **Solution Intent & Architecture** — Solution Architect, system specifications, architecture compliance.
5. **AI-Native Team SDLC** — Analysis, architecture, implementation, QA, deployment.
6. **Meta-Agent Governance** — Rule/workflow/skill generation, compliance auditing, PR validation.
7. **Quality & Security gating** — Built-in quality, AppSec scans, threat modeling, policy enforcement.
8. **Backlog Bus** — Cross-agent task handoff via `.backlog/`.
9. **Mermaid Visualization Library** — AI-readable/generatable diagrams for Portfolio, Solution, Program, Team levels.

## 8. Security & Compliance
- **LLM data policy:** Local-LLM first / within protected contour for strategic data
- **Authentication / authorization approach for SALSA users:** OAuth

## 9. Backlog & Git Conventions
- **Issue tracker:** GitHub Issues (open-source core).
- **Branching convention:** Feature branches from `main` with descriptive prefixes (`feat/`, `fix/`, `docs/`).
- **Backlog file naming convention:** `NNN-short-slug.md` inside `.backlog/`.
- **Human review gates:** Mandatory Human-in-the-Loop at every level (strategy → portfolio → program → team → code → QA).