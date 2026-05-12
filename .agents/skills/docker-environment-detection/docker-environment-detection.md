# Docker Environment Detection Skill

## Intent
Automatically detect and configure Docker environment with Windows + WSL2 support. Provide cross-platform Docker command execution with proper fallback strategies.

## Pre-conditions
- Programmer agent activated for Go service development
- Docker operations required (development, testing, deployment)
- Need for cross-platform compatibility (Windows/Linux/Mac)
- Access to execute_command tool for environment detection

## Step-by-Step Logic

### 1. Operating System Detection
1. **Detect Current OS:**
   - Use `runtime.GOOS` or system commands to identify Windows/Linux/Mac
   - Store OS type for subsequent environment setup

2. **Windows Special Handling:**
   - Check if running on Windows environment
   - Prepare for WSL2 detection and redirection

### 2. Docker Availability Check
1. **Native Docker Detection:**
   - Execute `docker --version` command
   - Execute `docker compose version` or `docker-compose --version`
   - Check if Docker daemon is running with `docker info`

2. **Windows WSL2 Docker Detection:**
   - If on Windows and native Docker unavailable:
   - Execute `wsl --list --verbose` to check WSL2 availability
   - Execute `wsl -e docker --version` to check Docker in WSL2
   - Execute `wsl -e docker info` to verify Docker daemon in WSL2

### 3. Environment Configuration
1. **Select Execution Strategy:**
   - **Linux/Mac**: Use native Docker commands
   - **Windows + Docker Desktop**: Use native commands
   - **Windows + WSL2 Docker**: Use WSL2 redirection
   - **No Docker**: Set unavailable flag

2. **Configure Command Templates:**
   - Native: `docker compose up -d`
   - WSL2: `wsl -e docker compose up -d`
   - With path handling for cross-platform

### 4. Docker Command Execution
1. **Command Wrapper Creation:**
   - Create wrapper function for Docker operations
   - Auto-prepend WSL prefix when needed
   - Handle path translations between Windows and WSL2

2. **Error Handling:**
   - Detect Docker permission issues
   - Provide guidance for Docker setup
   - Suggest next steps for unavailable Docker

### 5. Fallback Strategy Implementation
1. **When Docker Unavailable:**
   - Display clear message about Docker requirements
   - Suggest installation steps for Windows + WSL2
   - Pause further operations requiring Docker
   - Provide alternative development approaches

2. **Development Mode Adaptation:**
   - Switch to in-memory database for testing
   - Use mock services for external dependencies
   - Continue with non-Docker development tasks

## Quality Gates

### Environment Detection
- [ ] OS correctly identified (Windows/Linux/Mac)
- [ ] Docker availability properly detected
- [ ] WSL2 status checked on Windows
- [ ] Command execution strategy selected

### Command Execution
- [ ] Docker commands execute correctly in detected environment
- [ ] WSL2 redirection works on Windows
- [ ] Path handling works cross-platform
- [ ] Error messages are informative

### Fallback Handling
- [ ] Clear message displayed when Docker unavailable
- [ ] Development alternatives suggested
- [ ] Workflow properly paused for manual setup
- [ ] Recovery instructions provided

## Implementation Patterns

### Pattern 1: OS Detection
```go
func DetectEnvironment() (*Environment, error) {
    env := &Environment{}
    
    if runtime.GOOS == "windows" {
        env.OS = "windows"
        env.IsWSLAvailable = checkWSLAvailability()
        env.DockerInWSL = checkDockerInWSL()
    } else {
        env.OS = runtime.GOOS
    }
    
    env.NativeDocker = checkNativeDocker()
    env.ExecutionStrategy = selectStrategy(env)
    
    return env, nil
}
```

### Pattern 2: Docker Command Wrapper
```go
func ExecuteDockerCommand(ctx context.Context, env *Environment, command string, args ...string) error {
    var fullCommand string
    
    switch env.ExecutionStrategy {
    case "native":
        fullCommand = fmt.Sprintf("docker %s %s", command, strings.Join(args, " "))
    case "wsl2":
        fullCommand = fmt.Sprintf("wsl -e docker %s %s", command, strings.Join(args, " "))
    default:
        return fmt.Errorf("docker not available in current environment")
    }
    
    return executeCommand(ctx, fullCommand)
}
```

### Pattern 3: Environment Validation
```go
func ValidateDockerEnvironment(env *Environment) error {
    if env.ExecutionStrategy == "unavailable" {
        return &DockerUnavailableError{
            Message: "Docker is not available. Please install Docker Desktop or Docker in WSL2",
            Suggestions: []string{
                "Install Docker Desktop for Windows",
                "Install Docker in WSL2: curl -fsSL https://get.docker.com | sh",
                "Ensure Docker daemon is running",
            },
        }
    }
    return nil
}
```

## Error Handling Strategies

### Docker Not Found Error
```go
type DockerUnavailableError struct {
    Message     string
    Suggestions []string
}

func (e *DockerUnavailableError) Error() string {
    suggestion := strings.Join(e.Suggestions, "\n- ")
    return fmt.Sprintf("%s\n\nSuggestions:\n- %s", e.Message, suggestion)
}
```

### WSL2 Detection Error
- Provide WSL2 installation link
- Show command to enable WSL2: `wsl --install`
- Suggest Ubuntu distribution install

### Permission Error
- Suggest adding user to docker group
- Provide Docker Desktop restart instructions
- Show sudo alternative for Linux

## Integration Points

### With Go Service Generation
- Auto-detect environment before Docker operations
- Use wrapper functions for all Docker commands
- Provide environment-specific Dockerfile generation

### With Programmer Workflow
- Add environment check as prerequisite step
- Pause workflow if Docker unavailable
- Resume workflow after Docker setup

### With Testing Infrastructure
- Auto-select Docker-based or in-memory testing
- Configure test databases based on environment
- Provide fallback test strategies

## Output Format

### Environment Detection Report
```markdown
# Docker Environment Detection Report

## Environment Information
- **Operating System**: Windows/Linux/Mac
- **Docker Availability**: Available/Unavailable
- **WSL2 Status**: Available/Not Applicable
- **Execution Strategy**: Native/WSL2/Unavailable

## Docker Commands Status
- **docker**: Available/Not Found
- **docker compose**: Available/Not Found
- **Docker Daemon**: Running/Stopped

## Recommendations
[Specific guidance based on environment]
```

### Error Message Template
```markdown
⚠️ Docker Environment Issue

**Problem**: Docker is not available in your current environment.

**Detected Environment**: Windows with WSL2 not configured

**Next Steps**:
1. Install WSL2: `wsl --install`
2. Install Docker in WSL2: Follow official Docker guide
3. Restart your terminal
4. Run the command again

**Alternative**: Continue development without Docker (limited functionality)
```

## Success Criteria
- Environment accurately detected across platforms
- Docker commands execute successfully in supported environments
- Clear, actionable error messages when Docker unavailable
- Proper workflow pausing and resumption
- Developer can easily follow setup instructions

## Usage Instructions

### Before Docker Operations
Always call `DetectEnvironment()` first:
```go
env, err := docker.DetectEnvironment()
if err != nil {
    return fmt.Errorf("environment detection failed: %w", err)
}

if err := docker.ValidateDockerEnvironment(env); err != nil {
    // Display error and pause operations
    return err
}
```

### Execute Docker Commands
Use the wrapper for all Docker operations:
```go
err := docker.ExecuteDockerCommand(env, "compose", "up", "-d", "postgres")
if err != nil {
    return fmt.Errorf("docker command failed: %w", err)
}
```

### Error Recovery
Always check for DockerUnavailableError:
```go
if dockerErr, ok := err.(*docker.DockerUnavailableError); ok {
    // Display user-friendly message and pause
    return dockerErr
}
```

---
**Note**: This skill ensures cross-platform Docker compatibility and provides clear guidance when Docker is unavailable. Integration with other skills should always use the wrapper functions for consistent behavior.
