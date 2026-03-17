# SoClose Update - CLAUDE.md Generator

> Copy this prompt and paste it into Claude Code to generate an optimized CLAUDE.md
> tailored to your project.

## Prompt

```
Analyze this entire project and generate an optimized CLAUDE.md file at the root.

The CLAUDE.md must contain:

## 1. Project Identity
- Name, role, exact detected stack (including versions)
- Architecture overview (services, ports, external dependencies)
- Critical files that should never be touched without a prior plan

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
Infer from the codebase:
- Naming conventions used
- Architectural patterns in place (e.g. service layer, repository pattern, etc.)
- What is already broken or fragile (visible tech debt)
- Dev/build/test/deploy commands used in this project
- Critical env variables detected (.env.example or references in code)

## 7. Core Principles (global)
- Simplicity First: make every change as simple as possible, minimal code impact
- No Laziness: find root causes, no temporary fixes, senior developer standards
- Minimal Impact: changes should only touch what's necessary, avoid introducing bugs
- Never use em dashes in any output (use -- instead)
- Ollama-first for any local LLM calls (RTX 4070 available)

After generating CLAUDE.md, also create:
- tasks/todo.md (empty with project header)
- tasks/lessons.md (empty with project header)

Do not ask for confirmation, generate the 3 files directly.
```
