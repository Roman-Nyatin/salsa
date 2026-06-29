# Workflow: Analyst Agent

## Phase 1: Intake & Context Loading
1. **Read Backlog Task:** Load active `.backlog/*.md` file assigned to Analyst
2. **Load Domain Context:** Read `/docs/domain/glossary.md` for existing Ubiquitous Language
3. **Check Constraints:** Review `/.agents/memory-bank/project-brief.md` for domain boundaries

## Phase 2: Requirements Elicitation
4. **Interview Human:** Ask clarifying questions about intent, actors, and success criteria
5. **Draft Use Cases:** Create markdown files in `/docs/domain/usecases/` following template:
   - Title and ID
   - Actor(s)
   - Preconditions
   - Main Success Scenario (numbered steps)
   - Alternative Flows
   - Postconditions
   - Acceptance Criteria (Given/When/Then)

## Phase 3: Domain Modeling
6. **Update Glossary:** Add new terms to `/docs/domain/glossary.md` with:
   - Term name (English)
   - Definition
   - Context/Usage
   - Related terms
7. **Create UI Mocks:** If applicable, describe UI in markdown (no code, narrative + ASCII or reference to external mock tool)

## Phase 4: Quality Gate & Handoff
8. **Self-Review:** Verify acceptance criteria are testable and unambiguous
9. **Present to Human:** Display drafts for approval
10. **Await HITL Approval:** Pause for human sign-off
11. **Append Links:** Add artifact links to active `.backlog/` task
12. **Update Memory Bank:** Record completion in `/.agents/memory-bank/active-context.md`

## Phase 5: Architect Handoff
13. **Signal Completion:** Notify that use cases are ready for Architect Agent
14. **Provide Context Summary:** Brief summary of key decisions and constraints for next agent
