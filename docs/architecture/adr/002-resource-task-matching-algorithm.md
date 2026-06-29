# ADR 002: Resource-Task Matching Algorithm for PM Agent

## Status
Proposed

## Date
2026-06-29

## Context
The SALSA project requires a PM (Project Manager) Agent to perform intelligent task assignment based on participant skills and time constraints. The project involves:
- 8 team members with limited time budgets (2-3 hours/week)
- 8-week deadline
- Crowdsourced contribution model
- Skill-based assignment requirement (not pull model)

We need to choose an optimal algorithm for matching tasks to performers.

## Decision
We will use a **Greedy Algorithm with Local Search Optimization** for resource-task matching.

---

## Algorithm Design

### 1. Score Calculation

Each task-performer pair receives a score based on four factors:

```mermaid
flowchart TD
    A[Task-Performer Pair] --> B[Skill Match<br/>0-10]
    A --> C[Experience Weight<br/>x1.0-2.0]
    A --> D[Availability Factor<br/>0-1]
    A --> E[History Bonus<br/>optional]
    
    B --> F[Final Score]
    C --> F
    D --> F
    E --> F
    
    F --> G[Score = Skill × Experience × Availability × History]
```

**Score Formula:**
```
Final Score = Skill_Match × Experience_Weight × Availability_Factor × History_Bonus
```

### 2. Greedy Assignment Process

```mermaid
flowchart TD
    A[Start Assignment] --> B[Sort Tasks by Criticality]
    B --> C{More Tasks?}
    C -->|Yes| D[Get Next Task]
    C -->|No| M[End]
    D --> E[Find Highest Score Performer]
    E --> F{Constraints OK?}
    F -->|Yes| G[Assign Task]
    F -->|No| H[Find Next Best]
    H --> F
    G --> I[Update Time Budget]
    I --> C
    
    style G fill:#90EE90
    style H fill:#FFE4B5
```

### 3. Local Search Optimization

```mermaid
flowchart TD
    A[After Greedy] --> B[Try Swap Two Performers]
    B --> C{Swap Improves Score?}
    C -->|Yes| D[Keep Swap]
    C -->|No| E[Revert Swap]
    D --> F[Iteration +1]
    F --> G{Max Iterations<br/>or No Improvement?}
    G -->|No| B
    G -->|Yes| H[End Optimization]
    E --> G
    
    style D fill:#90EE90
    style H fill:#87CEEB
```

### 4. Constraints Handling

```mermaid
graph TD
    subgraph Hard Constraints
        A1[Time Budget<br/>cannot exceed]
        A2[Task Dependencies<br/>must satisfy]
        A3[Required Skills<br/>minimum threshold]
    end
    
    subgraph Soft Constraints
        B1[Performer Preferences<br/>flexible]
        B2[Load Balancing<br/>across team]
    end
    
    A1 --> C[Assignment Validation]
    A2 --> C
    A3 --> C
    B1 --> D[Score Adjustment]
    B2 --> D
    C --> E[Final Assignment]
    D --> E
    
    style A1 fill:#FF6B6B
    style A2 fill:#FF6B6B
    style A3 fill:#FF6B6B
    style B1 fill:#FFE66D
    style B2 fill:#FFE66D
```

---

## Comparison: Pros and Cons

### 1. Greedy + Local Search (Chosen) ✓

```mermaid
pie title Why We Chose This Approach
    "Simple to implement" : 20
    "Handles constraints naturally" : 25
    "Fast execution" : 15
    "Transparent reasoning" : 20
    "Flexible to changes" : 20
```

**Pros:**
- ✅ Simple to implement in prompt-based AI agent
- ✅ Handles real-world constraints naturally (time budget, dependencies)
- ✅ Fast execution (O(n²) for n tasks × m performers)
- ✅ Provides "good enough" solutions for 30-40 tasks
- ✅ Transparent reasoning process (AI can explain each decision)
- ✅ Flexible to add new constraints without algorithm redesign

**Cons:**
- ⚠️ May miss global optimum (local vs global maximum)
- ⚠️ Sensitive to task ordering
- ⚠️ No formal guarantee of optimality
- ⚠️ Requires careful constraint definition

---

### 2. Hungarian Algorithm

```mermaid
flowchart LR
    subgraph Problem
        T1[Task 1] --- P1[Person 1]
        T1 --- P2[Person 2]
        T2[Task 2] --- P1
        T2 --- P2
    end
    
    style Problem fill:#FFE4E1
```

**Pros:**
- ✅ Guarantees optimal solution for 1-to-1 assignment
- ✅ Well-studied, proven algorithm
- ✅ Polynomial time complexity O(n³)

**Cons:**
- ❌ Requires 1-to-1 mapping (participants can do multiple tasks)
- ❌ Doesn't handle time budget constraints natively
- ❌ Doesn't account for task dependencies
- ❌ Doesn't support soft preferences

---

### 3. Linear Programming (Simplex)

```mermaid
flowchart TD
    A[Define Variables] --> B[Set Objective Function]
    B --> C[Add Constraints]
    C --> D[Run Solver]
    D --> E[Get Optimal Solution]
    
    style A fill:#E0FFFF
    style B fill:#E0FFFF
    style C fill:#E0FFFF
    style D fill:#FFD700
    style E fill:#90EE90
```

**Pros:**
- ✅ Handles all types of constraints mathematically
- ✅ Guarantees optimal solution
- ✅ Flexible objective function

**Cons:**
- ❌ Complex to implement in AI agent
- ❌ Requires numerical solver
- ❌ Overkill for small projects (~30 tasks)
- ❌ Less transparent for AI reasoning

---

### 4. CSP Solver

```mermaid
flowchart TD
    A[Define Domain] --> B[Define Variables]
    B --> C[Define Constraints]
    C --> D[Search for Solution]
    D --> E[Constraint Propagation]
    E --> D
    
    style A fill:#F0FFF0
    style C fill:#F0FFF0
    style E fill:#98FB98
```

**Pros:**
- ✅ Natural constraint modeling
- ✅ Built-in constraint propagation
- ✅ Declarative specification

**Cons:**
- ❌ Requires specialized libraries
- ❌ May be slow for large search spaces
- ❌ Complex setup for simple use cases
- ❌ Less intuitive for prompt-based implementation

---

## Summary Comparison Table

```mermaid
gantt
    title Algorithm Complexity Comparison
    dateFormat X
    axisFormat %s
    
    section Greedy + Local Search
    Implementation    : 0, 2
    Execution Time    : 0, 3
    Constraint Handling: 0, 2
    
    section Hungarian
    Implementation    : 0, 4
    Execution Time    : 0, 5
    Constraint Handling: 0, 8
    
    section Linear Programming
    Implementation    : 0, 7
    Execution Time    : 0, 6
    Constraint Handling: 0, 2
    
    section CSP Solver
    Implementation    : 0, 6
    Execution Time    : 0, 7
    Constraint Handling: 0, 3
```

| Algorithm | Optimal | Handles Constraints | Implementation Complexity | Best For |
|-----------|---------|-------------------|-------------------------|----------|
| **Greedy + Local Search** | Near-optimal | ✓ Easy | Low | Our project ✓ |
| Hungarian Algorithm | ✓ Yes | ✗ Hard | Medium | 1-to-1 simple matching |
| Linear Programming | ✓ Yes | ✓ Easy | High | Large complex projects |
| CSP Solver | ✓ Yes | ✓ Easy | High | Academic/Research |

---

## Visual: Why Greedy + Local Search for Our Project?

```mermaid
graph TD
    subgraph Our Context
        A[8 Team Members] --> B[Limited Time<br/>2-3 hrs/week]
        C[30-40 Tasks] --> D[8 Week Deadline]
        E[Crowdsourced] --> F[Skill-Based<br/>Assignment Required]
    end
    
    subgraph Why Greedy Works
        B --> G[Handles Time<br/>Constraints]
        D --> H[Fast Enough<br/>for Deadlines]
        F --> I[Transparent<br/>Reasoning]
    end
    
    G --> J[✓ Perfect Fit]
    H --> J
    I --> J
    
    style J fill:#90EE90,stroke:#228B22,stroke-width:3px
```

---

## Consequences

### Positive 🎉
- Simple to implement in prompt-based AI agent
- Handles real-world constraints naturally
- Fast execution (O(n²) for n tasks × m performers)
- Provides "good enough" solutions for 30-40 tasks

### Negative ⚠️
- May miss global optimum (local vs global maximum)
- Sensitive to task ordering
- No formal guarantee of optimality

---

## Implementation Notes

The PM Agent should:

1. **Parse** member profiles from `.members/` directory
2. **Extract** skills, time budgets, experience levels
3. **Build** task requirements from WBS (Work Breakdown Structure)
4. **Calculate** scores using the formula above
5. **Run** greedy assignment
6. **Apply** local search optimization
7. **Output** assignment map with rationale

---

## References
- Hungarian Algorithm: Kuhn (1955)
- Local Search: Glover & Kochenberger (2003)
- TF-IDF: Salton & Buckley (1988)
