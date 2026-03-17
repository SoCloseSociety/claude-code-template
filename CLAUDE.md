# CLAUDE.md - SoClose Project Template

> Ce fichier est lu automatiquement par Claude Code au demarrage de chaque session.
> Adaptez la section "Project Identity" et "Project-Specific Rules" a chaque projet.

## 1. Project Identity

- **Nom**: [NOM DU PROJET]
- **Role**: [DESCRIPTION COURTE]
- **Stack**: FastAPI + React 19 + TypeScript + Vite + Supabase + Redis
- **Runtime**: Docker on VPS (32c/64GB/RTX 4070)
- **Architecture**: [SERVICES, PORTS, DEPENDANCES EXTERNES]
- **Fichiers critiques**: [FICHIERS A NE JAMAIS TOUCHER SANS PLAN]

## 2. Workflow Orchestration

### Plan Node Default
- Enter plan mode for ANY non-trivial task (3+ steps or architectural decisions)
- If something goes sideways, STOP and re-plan immediately -- never keep pushing
- Write detailed specs upfront before touching code
- Use plan mode for verification steps, not just building

### Subagent Strategy
- Use subagents liberally to keep main context window clean
- Offload research, exploration, parallel analysis to subagents
- One task per subagent for focused execution

### Self-Improvement Loop
- After any correction from user: update `tasks/lessons.md` with the pattern
- Write rules that prevent the same mistake from recurring
- Review `tasks/lessons.md` at session start

## 3. Verification Before Done

- Never mark a task complete without proving it works
- Ask: "Would a senior engineer approve this?"
- Run tests, check logs, demonstrate correctness
- Diff behavior between main and your changes when relevant

## 4. Autonomous Bug Fixing

- When given a bug report: fix it, no hand-holding
- Point at logs, errors, failing tests -- resolve them
- Zero context switching required from the user

## 5. Task Management

1. **Plan First**: Write plan to `tasks/todo.md` with checkable items
2. **Verify Plan**: Check in before starting implementation
3. **Track Progress**: Mark items complete as you go
4. **Explain Changes**: High-level summary at each step
5. **Document Results**: Add review section to `tasks/todo.md`
6. **Capture Lessons**: Update `tasks/lessons.md` after corrections

## 6. Project-Specific Rules

> A remplir apres analyse du codebase avec la commande soclose-update.

- **Conventions de nommage**: [A DEDUIRE]
- **Patterns architecturaux**: [A DEDUIRE - ex: service layer, repository pattern]
- **Dette technique visible**: [A DEDUIRE]
- **Commandes dev/build/test/deploy**: [A DEDUIRE]
- **Variables d'env critiques**: [A DEDUIRE depuis .env.example ou code]

## 7. Core Principles (global)

- **Simplicity First**: Make every change as simple as possible, minimal code impact
- **No Laziness**: Find root causes, no temporary fixes, senior developer standards
- **Minimal Impact**: Changes should only touch what's necessary, avoid introducing bugs
- **Never use em dashes** in any output (use -- instead)
- **Ollama-first** for any local LLM calls (RTX 4070 available)
