# SoClose Update - Generateur CLAUDE.md

> Copiez ce prompt et collez-le dans Claude Code pour generer un CLAUDE.md optimise
> adapte a votre projet.

## Prompt

```
Analyse l'integralite de ce projet et genere un fichier CLAUDE.md optimise a la racine.

Le CLAUDE.md doit contenir :

## 1. Project Identity
- Nom, role, stack exact detecte (versions comprises)
- Architecture overview (services, ports, dependances externes)
- Fichiers critiques a ne jamais toucher sans plan prealable

## 2. Workflow Orchestration
- Enter plan mode for ANY non-trivial task (3+ steps or architectural decisions)
- If something goes sideways, STOP and re-plan immediately -- never keep pushing
- Write detailed specs upfront before touching code
- Use subagents for research, exploration, parallel analysis -- one task per subagent
- After any correction from user: update tasks/lessons.md with the pattern

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
1. Plan First: write plan to tasks/todo.md with checkable items
2. Verify Plan: check in before starting implementation
3. Track Progress: mark items complete as you go
4. Explain Changes: high-level summary at each step
5. Document Results: add review section to tasks/todo.md
6. Capture Lessons: update tasks/lessons.md after corrections

## 6. Project-Specific Rules
Deduis depuis le codebase :
- Conventions de nommage utilisees
- Patterns architecturaux en place (ex: service layer, repository pattern, etc.)
- Ce qui est deja casse ou fragile (dette technique visible)
- Les commandes de dev/build/test/deploy utilisees dans ce projet
- Variables d'env critiques detectees (.env.example ou references dans le code)

## 7. Core Principles (global)
- Simplicity First: make every change as simple as possible, minimal code impact
- No Laziness: find root causes, no temporary fixes, senior developer standards
- Minimal Impact: changes should only touch what's necessary, avoid introducing bugs
- Never use em dashes in any output (use -- instead)
- Ollama-first for any local LLM calls (RTX 4070 available)

Apres avoir genere CLAUDE.md, cree aussi :
- tasks/todo.md (vide avec header du projet)
- tasks/lessons.md (vide avec header du projet)

Ne me demande pas de confirmation, genere directement les 3 fichiers.
```
