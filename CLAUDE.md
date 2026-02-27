# CLAUDE.md

## Project Overview

This is an **agentic product development team** workspace. It uses specialized AI agents
to handle the full software development lifecycle: requirements, architecture, implementation,
testing, review, and documentation.

> **Project-specific configuration** (tech stack, commands, directory layout) lives in
> [`PROJECT.md`](PROJECT.md). All agents read it automatically.

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

### Core Workflows
- `/new-feature [description]` -- Full feature workflow: PRD → design → implement → test → review
- `/fix-bug [description]` -- Bug workflow: investigate → fix → test → review (supports GitHub issue IDs)
- `/review-code` -- Run code review on current changes

### Plan/Execute Loop
- `/plan [feature]` -- Create a detailed implementation plan with codebase analysis
- `/execute [plan-path]` -- Implement from a plan file, task by task with validation
- `/prime` -- Load project context (structure, docs, recent activity)
- `/commit` -- Stage and create an atomic commit with conventional prefix

### Validation & Process Improvement
- `/validation:validate` -- Full project health check (lint, types, tests, build, code quality)
- `/validation:execution-report [plan-path]` -- Post-implementation report: what was built, divergences from plan
- `/validation:system-review [plan] [report]` -- Meta-analysis: plan vs. execution, process improvements

### GitHub Issue Integration
- `/github-issue:rca [issue-id]` -- Investigate a GitHub issue, create RCA document at `docs/rca/`

## Directory Structure

```
.claude/
  agents/           -- Agent definitions (role, tools, model, system prompt)
  commands/         -- Reusable workflow commands
    validation/     -- Validation and process improvement commands
    github-issue/   -- GitHub issue workflows (RCA)
  reference/        -- Tech-stack best practices (populated per project)
  settings.json     -- Shared team settings (committed)
  settings.local.json -- Personal settings (gitignored)
docs/
  prds/             -- Product Requirements Documents
  architecture/     -- Technical design documents
  plans/            -- Implementation plans (from /plan command)
  rca/              -- Root Cause Analysis documents (from /rca command)
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

- Error handling: never swallow errors silently
- All new business logic must have tests
- Functional patterns preferred over classes
- Run the validation command from `PROJECT.md` before every commit
- Follow language-specific rules defined in `PROJECT.md`

## Commands

See `PROJECT.md` for the full command table (install, dev, build, test, lint, typecheck, etc.).

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
- Bypass the project's type safety settings (see PROJECT.md)
- Skip writing tests for new logic
