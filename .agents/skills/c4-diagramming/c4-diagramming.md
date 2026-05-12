# C4 Diagramming Skill

## Intent
Provide standardized technical procedures for creating C4 model diagrams using Mermaid.js for the Java2Go migration project. This skill ensures consistency across all architectural visualizations.

## Pre-conditions
- Follow architectural standards defined in `.clinerules/architect.md`
- Project follows C4 Model (Context, Containers, Components, Code)
- All diagrams must use Mermaid.js syntax
- Language policy and formatting standards per architect.md apply

## Step-by-Step Logic

### 1. Context Level Diagram Creation
**Purpose**: Show system boundaries and external interactions

**Mermaid Template**:
```mermaid
graph TB
    "User (Пользователь)" --> "Java2Go Migration System"
    "Java2Go Migration System" --> "External System 1"
    "Java2Go Migration System" --> "External System 2"
    
    style "Java2Go Migration System" fill:#e1f5fe
    style "User (Пользователь)" fill:#f3e5f5
```

**Quality Gates**:
- [ ] All external systems clearly identified
- [ ] User interactions mapped
- [ ] System boundaries defined
- [ ] Node names in double quotes
- [ ] Russian labels with English terms

### 2. Container Level Diagram Creation
**Purpose**: Show application boundaries and technology stack

**Mermaid Template**:
```mermaid
graph TB
    subgraph "Java2Go Migration System"
        "Java Services (asis-java/)" --> "Migration Engine"
        "Migration Engine" --> "Go Services (tobe-go/)"
        "Migration Engine" --> "API Gateway"
        "API Gateway" --> "Database Layer"
    end
    
    "External Integration" --> "API Gateway"
    
    style "Java Services (asis-java/)" fill:#ffebee
    style "Go Services (tobe-go/)" fill:#e8f5e8
    style "Migration Engine" fill:#fff3e0
```

**Quality Gates**:
- [ ] All containers from project structure included
- [ ] Technology stack clearly labeled
- [ ] Data flow between containers defined
- [ ] External integrations mapped
- [ ] Color coding applied consistently

### 3. Component Level Diagram Creation
**Purpose**: Show internal structure and component interactions per container

**Mermaid Template**:
```mermaid
graph TB
    subgraph "Migration Engine Container"
        "Service Analyzer" --> "Pattern Mapper"
        "Pattern Mapper" --> "Code Generator"
        "Code Generator" --> "Validation Module"
        "Validation Module" --> "API Contract Validator"
    end
    
    subgraph "Data Layer"
        "Migration DB" 
        "Cache Layer"
    end
    
    "Pattern Mapper" --> "Migration DB"
    "Validation Module" --> "Cache Layer"
    
    style "Service Analyzer" fill:#e3f2fd
    style "Pattern Mapper" fill:#e8f5e8
    style "Code Generator" fill:#fff3e0
```

**Quality Gates**:
- [ ] All major components identified
- [ ] Internal relationships mapped
- [ ] External dependencies shown
- [ ] Component responsibilities clear
- [ ] Consistent naming conventions

### 4. Code Level Diagram Creation
**Purpose**: Show key code elements and their relationships (use sparingly)

**Mermaid Template**:
```mermaid
classDiagram
    class "MigrationService" {
        +analyzeServices()
        +generateSpec()
        +validateOutput()
    }
    
    class "JavaParser" {
        +parseSpringBoot()
        +extractDependencies()
        +mapAnnotations()
    }
    
    class "GoGenerator" {
        +generateStructs()
        +createHandlers()
        +setupMiddleware()
    }
    
    "MigrationService" --> "JavaParser"
    "MigrationService" --> "GoGenerator"
```

**Quality Gates**:
- [ ] Only for critical architectural decisions
- [ ] Key classes/interfaces only
- [ ] Relationships clearly defined
- [ ] Not over-detailed

## Diagram Standards

**NOTE**: Follow all architectural standards defined in `.clinerules/architect.md` including:
- Language policy (Russian with English terms)
- No emoji policy
- Entity naming conventions
- Professional formatting requirements

### Technical Naming Conventions
- **Files**: `{level}-{system-name}.md` (e.g., `context-java2go.md`)
- **Nodes**: `"Component Name (English Name)"`
- **Directories**: `docs/architecture/diagrams/{level}/`

### Color Coding Standard
- **Blue (#e1f5fe)**: System boundaries
- **Red (#ffebee)**: Source systems (Java)
- **Green (#e8f5e8)**: Target systems (Go)
- **Orange (#fff3e0)**: Processing/Transformation layers
- **Purple (#f3e5f5)**: User interfaces
- **Gray (#f5f5f5)**: External systems

### Mermaid Syntax Rules
1. **All node names in double quotes**: `"Component Name"`
2. **No Russian comments in Mermaid blocks**
3. **Use TB (top to bottom) or LR (left to right) consistently**
4. **Subgraphs for container boundaries**
5. **Style statements for visual clarity**

## Integration with Process

### Input Sources
- `project-brief.md` for system context
- Java source code analysis from `asis-java/`
- Go architecture decisions for `tobe-go/`
- Process overview from `.agents/memory-bank/`

### Output Destinations
- Context diagrams: `docs/architecture/diagrams/context/`
- Container diagrams: `docs/architecture/diagrams/containers/`
- Component diagrams: `docs/architecture/diagrams/components/`
- Code diagrams: `docs/architecture/diagrams/code/`

### Technical Validation Checklist
- [ ] Mermaid syntax is valid
- [ ] All node names in double quotes
- [ ] File naming conventions followed
- [ ] Directory structure correct
- [ ] Color coding applied consistently
- [ ] Subgraphs properly defined for containers

**Note**: For architectural validation (C4 hierarchy, cross-level consistency, language policy), use the validation process defined in `.clinerules/architect.md` under "C4 Model Consistency Validation".

## Quality Assurance

### Automated Checks
1. Mermaid syntax validation
2. File naming compliance
3. Directory structure validation
4. Language policy enforcement

### Manual Reviews
1. Architectural consistency across levels
2. Business logic representation accuracy
3. Integration completeness
4. Documentation clarity

## Troubleshooting

### Common Issues
- **Mermaid rendering fails**: Check for unescaped characters in node names
- **Inconsistent naming**: Verify English terms in parentheses
- **Cross-level misalignment**: Review C4 model hierarchy
- **Missing dependencies**: Map all external system interactions

### Resolution Steps
1. Validate Mermaid syntax using online editor
2. Cross-reference with project-brief.md requirements
3. Review architect.md standards
4. Consult process-overview.md for agent workflows

## Success Metrics
- All diagrams render correctly in Mermaid viewers
- 100% compliance with naming conventions
- Complete C4 model hierarchy maintained
- Zero policy violations (emojis, language, syntax)
- Clear traceability from context to code level
