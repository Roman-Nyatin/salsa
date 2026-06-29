# Создание PM-агента с помощью мета-агента 

## Постановка задачи
В рамках проекта SALSA (.backlog/README.md) требуется разработать огромное количество агентов для автоматизация SAFe® (Scaled Agile Framework).
Сроки создания сильно ограничены, составляют 8 недель от текущей даты. 
Проект будет выполняться с помощью краудсорс-подхода и представляет собой решение, которое будет храниться в публичном GitHub-репозитории.

Участники проекта представили свой опыт и скиллы, релевантные проекту, в папке .members.

Требуется создать PM-агента, который:
1. Создаст work breakdown structure проекта SALSA, сформировав бэклог команды 
2. Проанализирует информацию, хранящуюся в папке .members
3. Выберет наиболее оптимальных исполнителей для задач бэклога, с учетом опыта и скиллов участника проекта из папки .members
4. Концепция и предложения по созданию Agentic-SAFe приведены в документе docs/domain/safe-agentic-operating-system-proposal.md
5. Используй правила из .agents/rules/meta-agent.md
6. Использую Workflow из .agents/workflows/meta-agent.md

---

## Статус выполнения

### WBS Preparation — Завершено ✅

- **WBS Document:** [`.backlog/wbs-002-salsa.md`](.backlog/wbs-002-salsa.md)
- **Generated:** 29/06/2026
- **Total Deliverables:** ~40 L3 items
- **Estimated Effort:** ~308 hours
  - P0 (Critical): ~176 hours
  - P1 (High): ~108 hours
  - P2 (Nice-to-have): ~24 hours
- **Timeline:** 8 weeks
- **Quality Gate:** ⬜ Ожидает Human Approval

### Next Steps

- [ ] Human Approval на WBS
- [ ] Переход к Resource Matching (`.agents/workflows/pm-task-resource-matching.md`)
- [ ] Генерация Assignment Map (`docs/architecture/adr/assignment-002.md`)
