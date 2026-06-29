# Workflow: Programmer Agent

## Phase 1: Context Loading
1. **Read Specifications:** Load technical specs from `/docs/specs/` and C4 diagrams from `/docs/architecture/`
2. **Check Memory Bank:** Review `/.agents/memory-bank/project-brief.md` for constraints
3. **Validate Input:** Confirm that Architect phase and QA static analysis HITL gates were passed
4. **Understand Container Boundaries:** Identify independent vs dependent containers for implementation order

## Phase 2: Infrastructure Setup
5. **Environment Detection:** Execute `/.agents/skills/docker-environment-detection/docker-environment-detection.md` if Docker is needed
6. **Dev Environment:** Ensure local dev environment matches target stack (when stack is defined)

## Phase 3: Implementation (Hexagonal Architecture)
7. **Domain Layer:** Implement pure business logic in `/src/{container}/domain/`:
   - Entities with state and invariants
   - Domain services for complex operations
   - No external dependencies allowed
   - 100% unit test coverage required

8. **Application Layer:** Implement orchestration in `/src/{container}/application/`:
   - Commands and Queries (CQRS)
   - Handlers for commands/queries
   - Validators for input
   - Ports (interfaces) for external dependencies

9. **Infrastructure Layer:** Implement adapters in `/src/{container}/infrastructure/`:
   - Persistence adapters (DB, ORM)
   - External gateways (APIs, messaging)
   - Framework-specific code

10. **Bootstrap Layer:** Wire dependencies in `/src/{container}/bootstrap/`:
    - Dependency injection registration
    - Entry points (controllers, CLI, etc.)

## Phase 4: Testing
11. **Unit Tests:** Write tests in `/tests/` mirroring `/src/` structure
12. **Coverage Gates:** Ensure 90%+ coverage (100% for domain layer)
13. **Integration Tests:** Test container boundaries

## Phase 5: Environment Deployment
14. **Infra Manifests:** Create Docker, compose, or K8s manifests in `/infra/`
15. **One-Command Deploy:** Ensure `docker-compose up` or equivalent works

## Phase 6: Quality Gate & Handoff
16. **Self-Review:** Verify adherence to specs and architecture
17. **Present to Human:** Show implementation for review
18. **Await HITL Approval:** Pause for human sign-off
19. **Append Links:** Add artifact links to active `.backlog/` task
20. **Signal QA:** Trigger QA Agent for dynamic testing
21. **Update Memory Bank:** Record completion in `/.agents/memory-bank/active-context.md`
