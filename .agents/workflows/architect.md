# Workflow: Architect Agent

## Phase 1: Context & Alignment
1. **Load Analysis Artifacts:** Read use cases from `/docs/domain/usecases/` and glossary from `/docs/domain/glossary.md`
2. **Check Memory Bank:** Review `/.agents/memory-bank/project-brief.md` for constraints and `/.agents/memory-bank/process-overview.md` for standards
3. **Validate Input:** Confirm that Analysis phase HITL gate was passed

## Phase 2: C4 Model Construction
4. **Context Diagram:** Create/update `/docs/architecture/diagrams/context/context.md` with Mermaid C4 Context diagram
5. **Container Diagram:** Create/update `/docs/architecture/diagrams/containers/containers.md` with Mermaid C4 Container diagram
6. **Component Diagrams:** For each container, create `/docs/architecture/diagrams/containers/{container-name}/components.md` with Mermaid C4 Component diagrams
7. **Code Diagrams:** Deferred until implementation phase (only references to planned structure)

## Phase 3: Architecture Decision Records
8. **Identify Decisions:** For each significant architectural choice (framework, DB, communication pattern), create ADR
9. **Create ADRs:** Files in `/docs/architecture/adr/` following format:
   - Title and Date
   - Status (Proposed/Accepted/Deprecated)
   - Context
   - Decision
   - Consequences

## Phase 4: Technical Specifications
10. **Create Specs:** Low-level specs in `/docs/specs/` for Programmer Agent:
    - Container/Component boundaries
    - Interface contracts (method signatures, DTOs)
    - Data models (at conceptual level)
    - Required skills for Programmer Agent

## Phase 5: Threat Modeling
11. **Security Analysis:** Document threats and mitigations for each container
12. **Update ADRs:** Include security decisions

## Phase 6: Validation & Handoff
13. **Cross-Validation:** Verify C4 model consistency across levels (see rules/architect.md scoring)
14. **Present to Human:** Show architecture for review
15. **Await HITL Approval:** Pause for human sign-off
16. **Append Links:** Add artifact links to active `.backlog/` task
17. **Signal QA:** Trigger QA Agent for static contract analysis
18. **Signal Programmer:** After QA approval, handoff to Programmer Agent
