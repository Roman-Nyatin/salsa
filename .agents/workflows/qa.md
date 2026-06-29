# Workflow: QA Automation Agent

## Phase 1: Static Contract Analysis (Pre-Implementation)
1. **Read Artifacts:** Load specs from `/docs/specs/` and use cases from `/docs/domain/usecases/`
2. **Validate Alignment:** Check that specs cover all acceptance criteria from use cases
3. **Identify Gaps:** Report any missing specifications or ambiguous contracts
4. **Await HITL:** Wait for human approval before implementation proceeds

## Phase 2: Test Suite Generation (Post-Implementation)
5. **Acceptance Criteria Mapping:** Translate use case acceptance criteria to executable tests
6. **Test Plan Creation:** Create test plans in `/tests/`:
   - Unit test coverage validation
   - Integration test scenarios
   - Contract tests for APIs
   - Security test cases (if applicable)

## Phase 3: Environment Deployment
7. **Deploy SUT:** Use `/infra/` manifests to deploy System Under Test
8. **Stub Dependencies:** Deploy Component Stubs (DOC) for external dependencies
9. **Verify Health:** Ensure SUT is responding before testing

## Phase 4: Test Execution
10. **Run Unit Tests:** Validate domain layer coverage
11. **Run Integration Tests:** Test container interactions
12. **Regression Tests:** Run existing tests to detect breaking changes
13. **Performance Tests:** Execute load tests if defined
14. **Security Scans:** Run SAST/DAST tools if available

## Phase 5: Defect Reporting
15. **Analyze Failures:** Categorize failures (bug, spec issue, environment)
16. **Report Defects:** If bugs found, create structured defect reports in `.backlog/`
17. **Route to Programmer:** Assign defects back to Programmer Agent
18. **Retest:** After fixes, re-execute failed tests

## Phase 6: Quality Gate & Delivery
19. **Generate Report:** Create test execution summary with metrics
20. **Present to Human:** Show results for review
21. **Await HITL Approval:** Pause for final human sign-off
22. **Append Links:** Add test results to active `.backlog/` task
23. **Signal Delivery:** After approval, ready for merge to `main`
24. **Update Memory Bank:** Record completion in `/.agents/memory-bank/active-context.md`
