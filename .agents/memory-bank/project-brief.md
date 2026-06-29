# Project Brief: SALSA

## 1. Core Intent & Value Proposition
- **Product Name:** SALSA (Scaled Agentic Lean Secure Agile)
- **Product Vision:** Open-source implementation core of the SAFe Agentic Operating System (SAFe AOS). A Framework-as-Code extension to SAFe 6.0 that transforms the methodology from static documentation into an active, AI-native operating system, using Git (Markdown + Mermaid.js) as the single source of truth.
- **Target Audience:**
  - Enterprise C-level / Portfolio leadership
  - Lean Portfolio Management (LPM), Epic Owners
  - Release Train Engineers (RTE), Product Management, System Architects
  - Agile teams, SPCs, DevSecOps, SRE, AppSec engineers
- **Key Metric of Success:** Radical Time-to-Market reduction by 60–80%, elimination of hand-off delays, automated backlog readiness, built-in quality, lean overhead reduction.

### MVP Scope
- Open Source Core: Meta-agent prompts, role-specific skill library, Mermaid.js visualization templates for Portfolio & Solution Intent.
- End-to-end Private Demo: One hypothetical Epic flowing from Lean Business Case through AI-Native SDLC to automated release.

### Explicit Non-Scope
- Not a replacement for SAFe; a toolkit for SPCs that complements the methodology.
- Full enterprise UI/dashboard layer is an aspiration, not part of MVP.

## 2. Language & Documentation Policy
- **Agent system prompts, rules, workflows, skills:** English-only.
- **Project documentation, architecture, specs:** English-only.
- **Source code comments, logs, error messages:** English-only.
- **Git commit messages:** English, Conventional Commits.
- **Backlog / task tracker entries:** Russian and English allowed.
- **Transitional drafts / interview notes:** Russian permitted in `.backlog/` and `docs/domain/*Interview*.md` only.

## 3. Global Technical Stack Constraints
- **Current phase:** Markdown-only analysis and architecture.
- **Backend:** TBD — to be decided before implementation phase.
- **Frontend:** TBD — to be decided before implementation phase.
- **Database:** TBD — to be decided before implementation phase.
- **Message broker / event streaming:** TBD — to be decided before implementation phase.
- **Monorepo / multi-repo:** Keep current monorepo structure.

## 4. High-Level Domain Boundaries (DDD Contexts)
1. **Portfolio Management** — Strategic themes, investment horizons, Lean Business Case, WSJF, Epic Owner workflow.
2. **Lean Portfolio Orchestration** — LPM monitoring, budget guardrails, compliance alignment.
3. **ART / Program Coordination** — PI Planning, Program Board (Mermaid.js), dependencies, RTE workflow.
4. **Solution Intent & Architecture** — Solution Architect, system specifications, architecture compliance.
5. **AI-Native Team SDLC** — Analysis, architecture, implementation, QA, deployment.
6. **Meta-Agent Governance** — Rule/workflow/skill generation, compliance auditing, PR validation.
7. **Quality & Security gating** — Built-in quality, AppSec scans, threat modeling, policy enforcement.
8. **Backlog Bus** — Cross-agent task handoff via `.backlog/`.
9. **Mermaid Visualization Library** — AI-readable/generatable diagrams for Portfolio, Solution, Program, Team levels.

## 5. Operational Environment Specifications
- **Local dev sandbox engine:** TBD.
- **Target cloud infrastructure:** TBD.
- **AI runtime strategy:** Model-agnostic and deployment-agnostic. Participants may use their own local AI runtime (e.g., VS Code + OpenCode + OpenRouter/Kimi). The corporation eventually deploying agentic workforce will use its own protected contour.
