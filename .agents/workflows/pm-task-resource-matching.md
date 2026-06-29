# Workflow: PM Agent (Project Manager)

## Phase 1: Intake & Context Loading
1. **Read Backlog Task:** Load active `.backlog/*.md` file assigned to PM role
2. **Load Member Profiles:** Read all files from `.members/` directory to build team inventory:
   - Extract: name, time budget, roles, expertise, skills
3. **Load WBS (if exists):** Read Work Breakdown Structure for task decomposition
4. **Check Project Constraints:** Review timeline (8 weeks), team size, and deadlines

## Phase 2: Data Preparation
5. **Build Member Matrix:** Create table of members with:
   - Available hours per week
   - Skill ratings (0-10)
   - Experience levels
   - Role preferences

6. **Build Task List:** Extract from backlog:
   - Task ID and title
   - Required skills
   - Estimated effort (hours)
   - Dependencies on other tasks
   - Priority/criticality

7. **Calculate Skill Matches:** For each task-performer pair:
   ```
   Skill_Match = TF-IDF(task_requirements, performer_skills)
   ```

## Phase 3: Greedy Assignment (Algorithm Step 1)
8. **Sort Tasks by Criticality:** Order tasks by:
   - Dependencies first (tasks blocking others)
   - Business value
   - Effort (smaller tasks earlier for quick wins)

9. **Assign Tasks Iteratively:**
   For each task (in sorted order):
   a. Calculate scores for all performers using formula:
      ```
      Final Score = Skill_Match × Experience_Weight × Availability_Factor × History_Bonus
      ```
   b. Sort performers by score (descending)
   c. Check constraints:
      - Time budget not exceeded
      - Required skills met (minimum threshold)
      - Dependencies satisfied
   d. If valid → assign to top performer
   e. If not valid → try next best performer
   f. If no valid performer → mark as "Blocked" or "Needs Review"

10. **Update Time Budgets:** After each assignment, reduce performer's available time

## Phase 4: Local Search Optimization (Algorithm Step 2)
11. **Run Optimization Loop:**
    - Maximum 10 iterations
    - In each iteration:
      a. Try swapping assignments between two performers
      b. Calculate new total project score
      c. If score improves → keep swap
      d. If no improvement after full iteration → stop

12. **Validate Final Assignments:**
    - All hard constraints satisfied?
    - Any tasks remain unassigned?
    - Load distribution balanced?

## Phase 5: Output Generation
13. **Create Assignment Map:** Generate document in `/docs/architecture/adr/assignment-*.md`:
    ```markdown
    # Assignment Map - [Date]
    
    ## Task-Performer Matrix
    
    | Task ID | Task Title | Performer | Score | Effort | Week |
    |---------|------------|-----------|-------|--------|------|
    | T-001   | ...        | ...       | 8.5   | 3h     | 1    |
    
    ## Constraint Validation
    - Time budgets: ✓ All satisfied
    - Dependencies: ✓ All satisfied
    - Skills: ✓ All tasks have qualified performers
    ```

14. **Generate Weekly Distribution:**
    - Which tasks per week
    - Who is working on what
    - Critical path highlighting

15. **Calculate Total Project Score:** Sum of all individual assignment scores

## Phase 6: Quality Gate & Human Review
16. **Self-Review Checklist:**
    - [ ] All tasks assigned?
    - [ ] All hard constraints satisfied?
    - [ ] Score calculated correctly?
    - [ ] Dependencies mapped correctly?

17. **Present to Human:** Display assignment map in table format:
    - Show top 3 candidates for each task (with scores)
    - Highlight trade-offs made
    - Show blocked tasks (if any)

18. **Await HITL Approval:** Pause for human sign-off

19. **Append to Backlog:** Add assignment links to active `.backlog/` tasks

## Phase 7: Handoff & Monitoring
20. **Signal Completion:** Notify team of assignments
21. **Provide Context:**
    - Who is responsible for what
    - Key dependencies
    - First week's priorities

22. **Monitor & Adjust:** Be ready to re-run assignment if:
    - Scope changes
    - Team availability changes
    - New members join

---

## Quick Reference: Algorithm Summary

```
1. INPUT: Members (M), Tasks (T)
2. FOR each task t in T (sorted by criticality):
3.   FOR each member m in M:
4.     score[m] = calculate_score(t, m)
5.   SORT m by score DESC
6.   FOR each m in sorted:
7.     IF constraints_ok(t, m):
8.       assign(t, m)
9.       UPDATE time_budget(m)
10.      BREAK
11. REPEAT max 10 times:
12.  TRY swap any two assignments
13.  IF total_score_improved:
14.    KEEP swap
15.  ELSE:
16.    REVERT and STOP
17. OUTPUT: Assignment Map
```
