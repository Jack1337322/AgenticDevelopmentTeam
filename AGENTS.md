# AGENTS.md

> Universal agent instructions for all AI coding tools.
> Supported by: Claude Code, GitHub Copilot, Cursor, Codex, Devin, Factory, Gemini CLI, Jules, VS Code, Zed.

## Project Overview

Agentic product development team workspace. Multi-agent architecture with specialized
roles handling requirements, architecture, implementation, testing, review, and documentation.

**Tech Stack**: TypeScript (strict), Node.js, React, PostgreSQL, Vitest, Playwright

## Setup

```bash
pnpm install
cp .env.example .env
pnpm db:migrate
pnpm db:seed
pnpm dev
```

## Build & Test

| Task | Command |
|------|---------|
| Dev server | `pnpm dev` |
| Build | `pnpm build` |
| Unit tests | `pnpm test` |
| Single test | `pnpm test -- path/to/file.test.ts` |
| E2E tests | `pnpm test:e2e` |
| Coverage | `pnpm test:coverage` |
| Lint | `pnpm lint --fix` |
| Type check | `pnpm typecheck` |

## Architecture

```
src/
├── api/            # HTTP layer (routes, controllers, middleware)
├── services/       # Business logic (no HTTP awareness)
├── repositories/   # Data access (SQL queries, ORM calls)
├── models/         # Type definitions and validation schemas
├── utils/          # Pure utility functions
├── config/         # Environment and app configuration
└── ui/             # Frontend React components
    ├── components/ # Reusable UI components
    ├── pages/      # Page-level components
    ├── hooks/      # Custom React hooks
    └── stores/     # State management

docs/
├── prds/           # Product Requirements Documents
├── architecture/   # Technical design documents
└── templates/      # Document templates
```

**Data flow**: Route → Controller → Service → Repository → Database

## Code Style

- TypeScript strict mode, no `any` -- use `unknown` and narrow
- `const` over `let`, never `var`
- Named exports, no default exports
- Barrel files (`index.ts`) for module public APIs
- File naming: `kebab-case.ts` for modules, `PascalCase.tsx` for components
- Imports: external → internal → relative, separated by blank lines
- Functions under 30 lines; extract helpers when needed
- Error handling: use `Result<T, E>` pattern, never throw from services

## Testing

- Unit tests colocated as `*.test.ts` next to source files
- Integration tests in `tests/integration/`
- E2E tests in `tests/e2e/`
- Use factories and fixtures, not hardcoded test data
- Mock external services, never call real APIs in tests
- Every acceptance criterion from the PRD must have at least one test

## Security

- Auth: JWT tokens in httpOnly cookies
- Input validation: Zod schemas on all API endpoints
- SQL: parameterized queries only (ORM handles this)
- NEVER log tokens, passwords, or PII
- NEVER commit `.env`, credentials, or API keys
- NEVER disable security middleware for convenience

## Git Workflow

- Branches: `feat/description`, `fix/description`, `chore/description`
- Commits: conventional commits (`feat:`, `fix:`, `chore:`, `docs:`)
- PRs: require CI pass + human approval
- Squash merge to main

## Agent Workflow

Features flow through a defined pipeline:
1. **PRD** created by product-manager agent in `docs/prds/`
2. **Design doc** created by architect agent in `docs/architecture/`
3. **Implementation** by implementer agent on feature branch
4. **Tests** validated by tester agent
5. **Review** by code-reviewer agent
6. **Merge** approved by human

PRD templates are in `docs/templates/prd-template.md`.
