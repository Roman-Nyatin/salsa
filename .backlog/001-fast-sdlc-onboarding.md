# Онбординг fast-asdlc

## Постановка задачи
Требуется выполнить онбординг fast-asdlc в проект Scaled Agentic Lean Secure Agile (SALSA)

Используй роль: .agents/rules/meta-agent.md 
Используй видение: docs/domain/safe-agentic-operating-system-proposal.md
Используй промпт: .agents/fast-asdlc/BOOTSTRAP-PROMPT.md
Для provisioning'а агентов используй скилл: .agents/skills/tool-onboarding-opencode/tool-onboarding-opencode.md

## Статус: ВЫПОЛНЕНО

### Созданные артефакты

#### Memory Bank
- `/.agents/memory-bank/project-brief.md` — продуктовое видение, языковая политика, доменные границы
- `/.agents/memory-bank/process-overview.md` — процесс, матрица роль→инструмент, фазы SDLC
- `/.agents/memory-bank/active-context.md` — текущий контекст системы
- `/.agents/memory-bank/progress.md` — прогресс выполнения
- `/.agents/memory-bank/decision-log.md` — принятые решения

#### Agent Rules
- `/.agents/rules/analyst.md` — правила Analyst Agent
- `/.agents/rules/architect.md` — обновлены правила Architect Agent (добавлен OpenCode)
- `/.agents/rules/programmer.md` — обновлены правила Programmer Agent (добавлен OpenCode, Language Policy)
- `/.agents/rules/qa.md` — обновлены правила QA Agent (добавлен OpenCode, Language Policy)

#### Agent Workflows
- `/.agents/workflows/analyst.md` — workflow Analyst Agent
- `/.agents/workflows/architect.md` — workflow Architect Agent
- `/.agents/workflows/programmer.md` — workflow Programmer Agent
- `/.agents/workflows/qa.md` — workflow QA Agent

#### Tool Configuration
- `/.clinerules` — обновлены правила OpenCode с Language Policy и Role-to-Workspace mapping
- `/.agents/mcp/mcp-settings.json` — настройки MCP (placeholder)

## Следующие шаги
1. Создать первый продуктовый бэклог-айтем (например, анализ домена Portfolio Management)
2. Передать задачу Analyst Agent для начала Phase 1 (Analysis & Design)