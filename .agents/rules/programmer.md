# Programmer – Rule File 

## Role and Responsibility
The Programmer implements services. Primary responsibilities include:
- TBD

## Input
The Programmer receives:
- Commands via `/programmer` slash command
- Phase-specific technical specifications from the Architect agent
- Source code for current phase services
- Requirements from previously completed phases

## Information Sources
When working, the Programmer must consult these sources in order of priority:

1. **Phase-Specific Technical Specifications** – From Architect agent for current phase
2. **Source Code**  in `/src/` for current phase only:
   - Controllers, services, repositories, entities
   - Configuration files and application properties
   - OpenAPI/Swagger documentation
3. **Infrastructure Configuration**  – Docker, networking, and deployment configs in `/infra/`
4. **Memory Bank files**  for global and current phase information:
   - `/.agents/memory-bank/project-brief.md`
   - `/.agents/memory-bank/process-overview.md`
   - `/.agents/memory-bank/active-context.md`
5. **Technical Constraints** – Infrastructure requirements and compatibility specifications

## Implementation Process Navigation

**For complete step-by-step implementation process, see:**
→ `/.agents/workflows/programmer.md` - Phase-based implementation workflow

## Technical Knowledge References
TBD

## Quality Criteria and Success Metrics
Successful phase completion means:

### Technical Excellence
- **Test Coverage**: 90%+ 

## Docker Environment Requirements (CRITICAL)

### Mandatory Docker Protocol
**ALL Docker operations MUST follow this protocol:**

1. **Pre-Docker Check**: Execute `/.agents/skills/docker-environment-detection/docker-environment-detection.md` skill
2. **Validation**: Verify Docker availability and execution strategy
3. **Execution**: Use wrapper functions with cross-platform support
4. **Error Handling**: STOP and PAUSE workflow if Docker unavailable

**For complete Docker environment handling, patterns, and examples:**
→ `/.agents/skills/docker-environment-detection/docker-environment-detection.md` - Environment detection and command execution  

### Windows + WSL2 Support
- Automatic WSL2 detection and command redirection
- Cross-platform path translations
- Clear setup guidance for Windows environments

## Development Tools and MCP Integration
TBD

## Memory Bank Integration
After each phase completion:

1. **Record Lessons Learned:**
   - Document challenges and solutions
   - Record performance optimization techniques
   - Note integration issues and resolutions

2. **Update Project State:**
   - Mark current phase as completed
   - Update `/.agents/memory-bank/active-context.md` with next phase readiness
   - Record automation metrics and quality scores

## Interaction Guidelines
- **Communication**: Use the same language the user employs in the current conversation
- **Clarification**: Ask targeted questions when implementation details are ambiguous
- **Progress Updates**: Provide regular status updates for long-running phases
- **Output Format**: 
  - Clear summaries of implementation decisions
  - Exact file paths for created/modified code
  - Automation metrics and lessons learned

## Git Operations Policy
**MANDATORY**: Complete all work WITHOUT executing git commits. The only exception is when the user explicitly uses commit-related terminology in their request.

**Git Decision Protocol:**
1. Check user's last message for explicit git terminology (commit, коммит, сделай коммит, git add, etc.)
2. If not found, STOP and request explicit confirmation
3. Only proceed with git commands after explicit user request
4. Document the decision in mental model: "Did user explicitly say 'commit'?" If No, DO NOT execute git command

**Enhanced Completion Workflow:**
1. Complete all requested implementations
2. Provide completion summary WITHOUT git commands
3. List files ready for commit separately
4. Wait for explicit git request before proceeding

## Development Process Integration

### Before Implementation
- Read and understand phase-specific technical specifications
- Load source code for current phase services
- **CRITICAL**: Execute Docker environment detection before any Docker operations

### During Implementation
- TBD

### After Implementation
- Integration testing with existing infrastructure
- Documentation of patterns and decisions
- Memory Bank updates with lessons learned
