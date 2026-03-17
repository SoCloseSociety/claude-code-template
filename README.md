# Claude Code Template - SoClose

Template de configuration Claude Code pour les projets SoClose.

Inspire du prompt de Boris Cherny, adapte a notre stack et workflow.

## Contenu

- `CLAUDE.md` -- Template de configuration Claude Code (lu automatiquement a chaque session)
- `tasks/todo.md` -- Plan courant du projet
- `tasks/lessons.md` -- Erreurs passees et patterns a eviter
- `soclose-update.md` -- Prompt pour generer un CLAUDE.md adapte a un projet existant

## Utilisation

### Nouveau projet
1. Clonez ce repo ou copiez les fichiers dans votre projet
2. Editez `CLAUDE.md` section "Project Identity" et "Project-Specific Rules"
3. Claude Code lira automatiquement le fichier au demarrage

### Projet existant
1. Copiez le prompt dans `soclose-update.md` dans Claude Code
2. Il analysera le codebase et generera un CLAUDE.md adapte

## Stack par defaut
- FastAPI + React 19 + TypeScript + Vite + Supabase + Redis
- Docker on VPS (32c/64GB/RTX 4070)
- Ollama pour les LLM calls locaux
