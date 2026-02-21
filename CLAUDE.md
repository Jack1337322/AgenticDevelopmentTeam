# CLAUDE.md

## Project Overview

This is an **agentic product development team** workspace. It uses specialized AI agents
to handle the full software development lifecycle: requirements, architecture, implementation,
testing, review, and documentation.

## Agent Team Structure

This project uses Claude Code sub-agents defined in `.claude/agents/`. Each agent has a
specific role, tool access, and permission model. The team lead (your main Claude Code session)
delegates to specialists:

| Agent | Role | Model | When to Use |
|-------|------|-------|-------------|
| `product-manager` | PRDs, user stories, acceptance criteria | opus | Planning new features |
| `architect` | System design, API contracts, data models | opus | Technical design decisions |
| `implementer` | Code writing, feature implementation | inherit | Building features |
| `code-reviewer` | Quality, security, performance review | inherit | After code changes |
| `tester` | Test writing, coverage, validation | sonnet | Verifying acceptance criteria |
| `debugger` | Root cause analysis, bug fixing | inherit | Investigating bugs |
| `docs-writer` | API docs, architecture docs, changelogs | sonnet | Documentation tasks |

## Workflow Commands

Custom commands in `.claude/commands/`:
- `/new-feature [description]` -- Full feature workflow: PRD → design → implement → test → review
- `/fix-bug [description]` -- Bug workflow: investigate → fix → test → review
- `/review-code` -- Run code review on current changes

## Directory Structure

```
.claude/
  agents/           -- Agent definitions (role, tools, model, system prompt)
  commands/         -- Reusable workflow commands
  settings.json     -- Shared team settings (committed)
  settings.local.json -- Personal settings (gitignored)
docs/
  prds/             -- Product Requirements Documents
  architecture/     -- Technical design documents
  templates/        -- PRD and design doc templates
CLAUDE.md           -- This file (Claude-specific project context)
AGENTS.md           -- Universal agent instructions (all AI tools)
```

## Development Workflow

### Feature Development (idea → merge)

```
1. Human provides feature idea
2. product-manager agent → creates PRD in docs/prds/
3. Human reviews + approves PRD
4. architect agent → creates design doc in docs/architecture/
5. Human reviews + approves design
6. implementer agent → writes code on feature branch
7. tester agent → validates acceptance criteria, writes tests
8. code-reviewer agent → reviews all changes
9. Human reviews PR and merges
```

### Bug Fixing

```
1. Human describes the bug
2. debugger agent → investigates root cause
3. Human approves proposed fix
4. implementer agent → applies fix
5. tester agent → adds regression test
6. code-reviewer agent → reviews fix
7. Human reviews and merges
```

## Code Standards

- TypeScript strict mode, no `any` types
- Functional patterns preferred over classes
- Error handling: never swallow errors silently
- All new business logic must have tests
- Run validation before every commit: `pnpm test && pnpm typecheck && pnpm lint`

## Commands

```
pnpm install          # Install dependencies
pnpm dev              # Start dev server
pnpm build            # Production build
pnpm test             # Run all tests
pnpm test:coverage    # Tests with coverage report
pnpm typecheck        # TypeScript type checking
pnpm lint             # ESLint
pnpm lint:fix         # ESLint with auto-fix
pnpm db:migrate       # Run database migrations
pnpm db:seed          # Seed development data
```

## Git Workflow

- Branch naming: `feat/`, `fix/`, `chore/`, `refactor/` prefixes
- Commits: conventional commits (`feat:`, `fix:`, `chore:`, `docs:`)
- PRs require passing CI and human approval

## Boundaries

### ALWAYS (agents can do freely)
- Read any file in the project
- Run tests, linters, type checks
- Create/edit source files and test files
- Create branches and commits

### ASK FIRST (requires human approval)
- Add new dependencies
- Modify database schemas
- Change shared interfaces or API contracts
- Modify CI/CD configuration
- Delete files or directories

### NEVER
- Commit secrets, API keys, or credentials
- Modify existing migration files after they've been applied
- Push to main/master directly
- Bypass TypeScript strict mode
- Skip writing tests for new logic
