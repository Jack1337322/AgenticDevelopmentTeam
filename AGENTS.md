# AGENTS.md

> Universal agent instructions for all AI coding tools.
> Supported by: Claude Code, GitHub Copilot, Cursor, Codex, Devin, Factory, Gemini CLI, Jules, VS Code, Zed.

## Project Overview

Agentic product development team workspace. Multi-agent architecture with specialized
roles handling requirements, architecture, implementation, testing, review, and documentation.

**Tech Stack**: See `PROJECT.md` for language, runtime, framework, database, and tooling.

## Setup

See `PROJECT.md` for install, environment setup, and database commands.

## Build & Test

See `PROJECT.md` for the full command table (dev, build, test, lint, typecheck, etc.).

## Architecture

See `PROJECT.md` for the project directory structure and architecture pattern.

```
docs/
├── prds/           # Product Requirements Documents
├── architecture/   # Technical design documents
└── templates/      # Document templates
```

## Code Style

- Functions should have a single responsibility and stay short
- Use clear, descriptive names; no abbreviations
- Functional patterns preferred over classes
- Error handling: never swallow errors silently
- Follow the import ordering convention defined in `PROJECT.md`
- Follow file naming conventions from `PROJECT.md`
- Run the validation command from `PROJECT.md` before every commit
- See `PROJECT.md` for language-specific coding rules

## Testing

- Use factories and fixtures, not hardcoded test data
- Mock external services, never call real APIs in tests
- Every acceptance criterion from the PRD must have at least one test
- Follow test file naming and location conventions from `PROJECT.md`

## Security

- NEVER log tokens, passwords, or PII
- NEVER commit `.env`, credentials, or API keys
- NEVER disable security middleware for convenience
- Injection prevention appropriate to the tech stack (see `PROJECT.md`)
- See `PROJECT.md` for project-specific security rules

## Git Workflow

- Branches: `feat/description`, `fix/description`, `chore/description`
- Commits: conventional commits (`feat:`, `fix:`, `chore:`, `docs:`)
- PRs: require CI pass + human approval
- Squash merge to main

## Agent Workflow

See `CLAUDE.md` for the full agent team structure, workflow skills, and development pipeline.
PRD templates are in `docs/templates/`.
