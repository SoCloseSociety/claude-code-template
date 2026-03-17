# Claude Code Template - SoClose

Claude Code configuration template for SoClose projects.

Inspired by Boris Cherny's prompt, adapted to our stack and workflow.

## Contents

- `CLAUDE.md` -- Claude Code configuration template (automatically read at each session start)
- `tasks/todo.md` -- Current project plan
- `tasks/lessons.md` -- Past mistakes and patterns to avoid
- `soclose-update.md` -- Prompt to generate a CLAUDE.md tailored to an existing project

## Usage

### New project
1. Clone this repo or copy the files into your project
2. Edit `CLAUDE.md` sections "Project Identity" and "Project-Specific Rules"
3. Claude Code will automatically read the file on startup

### Existing project
1. Copy the prompt from `soclose-update.md` into Claude Code
2. It will analyze the codebase and generate a tailored CLAUDE.md

## Default Stack
- FastAPI + React 19 + TypeScript + Vite + Supabase + Redis
- Docker on VPS (32c/64GB/RTX 4070)
- Ollama for local LLM calls
