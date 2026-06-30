# Workflow: PM Agent - WBS Preparation

## Purpose
Create Work Breakdown Structure (WBS) for SALSA project (Agentic SAFe domain) within 8-week timeline. The WBS decomposes project scope into actionable deliverables that can be assigned to team members from `.members/`.

## Scope
- **Timeline:** 8 weeks (crowdsourced execution)
- **Domain:** Agentic SAFe (SAFe Agentic Operating System)
- **WBS Level:** L3 (deliverables)
- **Language (workflow):** English (per meta-agent rules)
- **Language (WBS artifacts in .backlog/):** Russian and English allowed (per project-brief.md)

---

## Phase 1: Context Loading

1. **Read Backlog Task:** Load `.backlog/002-pm-agent-creation.md` to understand PM-agent requirements
2. **Read Vision:** Load `docs/domain/safe-agentic-operating-system-proposal.md` to understand SAFe AOS concept
3. **Check Project Constraints:** Review timeline (8 weeks), team availability, and open-source nature
4. **Read Member Profiles:** Index all files from `.members/` directory:
   - Extract: name, time budget (hours/week), roles, expertise, skills
   - Build preliminary team capability matrix

---

## Phase 2: Scope Definition

5. **Define MVP Boundaries:** Based on safe-agentic-operating-system-proposal.md, identify what is IN scope:
   - **IN:** Meta-agent infrastructure, role-specific agent library (Analyst, Architect, Programmer, QA), Mermaid visualization templates, demo Epic through AI-Native SDLC
   - **OUT:** Full enterprise UI/dashboard layer, production deployment infrastructure

6. **Identify SAFe Layers:** Map deliverables to SAFe hierarchy:
   - **Portfolio Level:** Lean Business Case, Epic management, Strategic Themes
   - **Program Level (ART):** PI Planning artifacts, Program Board, RTE workflows
   - **Team Level (Agile Team):** AI-Native SDLC agents (Analyst, Architect, Programmer, QA)

7. **Define Domain Contexts:** Based on project-brief.md Section 4, identify target domains:
   - Portfolio Management
   - Lean Portfolio Orchestration
   - ART / Program Coordination
   - Solution Intent & Architecture
   - AI-Native Team SDLC
   - Meta-Agent Governance
   - Quality & Security Gating
   - Mermaid Visualization Library

---

## Phase 3: WBS Decomposition (L1-L3)

### L1: SAFe Levels
- Portfolio Management
- Program Coordination (ART)
- Team SDLC (Agile Team)
- Meta-Agent Infrastructure

### L2: Domain Groups
For each L1 element, decompose to L2 domain groups. Example:

**L1: Team SDLC (Agile Team)**
- L2: Analyst Agent Setup
- L2: Architect Agent Setup
- L2: Programmer Agent Setup
- L2: QA Agent Setup

### L3: Deliverables
For each L2 element, define specific deliverables (files, artifacts, configurations). Example:

**L2: Analyst Agent Setup**
- L3: `/.agents/rules/analyst.md` — Role identity and constraints
- L3: `/.agents/workflows/analyst.md` — Step-by-step execution workflow
- L3: `/.agents/skills/analysis-sop/*.md` — Skill SOPs

---

## Phase 4: Effort & Dependency Estimation

8. **Estimate Effort:** For each L3 deliverable, assign:
   - Estimated hours (based on complexity: Small <4h, Medium 4-8h, Large 8-16h, XL 16h+)
   - Difficulty rating (1-5)

9. **Map Dependencies:** For each L3 deliverable, identify:
   - Prerequisites (what must be completed first)
   - Blockers (what cannot start until X is done)
   - Parallel opportunities (what can run concurrently)

10. **Identify Critical Path:** Determine the longest dependency chain through the WBS

11. **Assign Priority:** Tag each deliverable:
    - **P0 (Critical):** Must be delivered for MVP
    - **P1 (High):** Important but can be deferred
    - **P2 (Nice-to-have):** Enhancement, not MVP-critical

---

## Phase 5: HITL Review

12. **Generate WBS Document:** Create markdown table in `.backlog/wbs-*.md`:
    ```markdown
    # WBS: SALSA Agentic SAFe — [Date]
    
    ## Overview
    - Total Deliverables: X
    - Estimated Total Effort: Y hours
    - Critical Path: Z weeks
    
    ## WBS Table
    
    | ID | Level | Deliverable | Effort | Priority | Dependencies |
    |----|-------|-------------|--------|----------|--------------|
    | WBS-001 | L1 | Portfolio Management | 16h | P0 | - |
    | WBS-001.1 | L2 | Lean Business Case Template | 4h | P0 | WBS-001 |
    ```

13. **Present to Human:** Display WBS in structured table format

14. **Await Approval:** Pause for human sign-off before proceeding to resource matching

---

## Phase 6: Handoff

15. **Update Backlog:** Append WBS reference to active `.backlog/002-pm-agent-creation.md`

16. **Signal Next Phase:** Notify that WBS is ready for:
    - Resource matching (`.agents/workflows/pm-task-resource-matching.md`)
    - Assignment generation (`docs/architecture/adr/assignment-*.md`)

---

## Quality Gate Checklist

- [ ] All SAFe levels covered (Portfolio / ART / Team)
- [ ] All domain contexts from project-brief.md represented
- [ ] All deliverables have effort estimates
- [ ] Dependencies mapped and critical path identified
- [ ] Priority tags assigned (P0/P1/P2)
- [ ] Human approval received
- [ ] WBS document written to `.backlog/`

---

## Quick Reference: WBS Structure

```
SALSA Project (Agentic SAFe)
├── L1: Portfolio Management
│   ├── L2: Epic Owner Workflows
│   ├── L2: Lean Portfolio Management
│   └── L2: Strategic Theme Tracking
├── L1: Program Coordination (ART)
│   ├── L2: PI Planning Artifacts
│   ├── L2: Program Board
│   └── L2: RTE Agent Setup
├── L1: Team SDLC (Agile Team)
│   ├── L2: Analyst Agent Setup
│   ├── L2: Architect Agent Setup
│   ├── L2: Programmer Agent Setup
│   └── L2: QA Agent Setup
└── L1: Meta-Agent Infrastructure
    ├── L2: Rule Generation System
    ├── L2: Workflow Automation
    └── L2: Skill Library
```
