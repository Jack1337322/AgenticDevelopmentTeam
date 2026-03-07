# Agentic Product Development Team

> Enterprise-grade agentic development workflow using Claude Code sub-agents.

---

## What This Is

A complete, ready-to-use setup for running an AI-powered product development team
using Claude Code. The team consists of specialized agents (product manager, architect,
developer, tester, reviewer, debugger, docs writer) that collaborate through 35 workflow
and domain skills to go from zero (no project) to production-ready code. Use `/bootstrap`
to scaffold a new project, then `/new-feature` to build features through the full pipeline.

## Files Created

```
AgenticDevelopmentTeam/
├── CLAUDE.md                              # Claude-specific project context
├── AGENTS.md                              # Universal agent instructions (all AI tools)
├── README.md                               # This file -- setup guide
├── .claude/
│   ├── settings.json                      # Shared permissions + agent teams flag
│   ├── settings.local.json                # Personal settings (gitignored)
│   ├── agents/
│   │   ├── product-manager.md             # PRD creation, story breakdown
│   │   ├── architect.md                   # System design, API contracts
│   │   ├── implementer.md                 # Code writing, feature implementation
│   │   ├── code-reviewer.md               # Quality, security, performance review
│   │   ├── tester.md                      # Test writing, coverage validation
│   │   ├── debugger.md                    # Root cause analysis, bug investigation
│   │   └── docs-writer.md                 # Documentation generation
│   └── skills/                            # Workflow skills (SKILL.md format)
│       ├── new-feature/SKILL.md           # /new-feature [description]
│       ├── fix-bug/SKILL.md               # /fix-bug [description]
│       ├── review-code/SKILL.md           # /review-code
│       ├── ... (27 workflow skills)       # See CLAUDE.md for full list
│       └── ... (8 domain skills)          # Auto-loaded background knowledge
└── docs/
    ├── templates/
    │   └── PRD-TEMPLATE.md                # Agent-optimized PRD template
    ├── prds/                              # Generated PRDs go here
    └── architecture/                      # Design documents go here
```

---

## How to Use

### Quick Start

1. Clone or copy this template into your project directory
2. Run `/bootstrap [project description]` -- this fills in PROJECT.md, scaffolds the project, installs deps, and validates
3. Start building with `/new-feature [description]`

#### Alternative: Manual Setup

If you prefer full control over the initial setup:

1. Copy this directory structure into your project
2. Fill in `PROJECT.md` with your tech stack, commands, directory layout, and conventions
3. Update `.claude/settings.json` with Bash permissions for your project's tools (see `PROJECT.md` Permissions Guidance)
4. Customize `CLAUDE.md` with any additional project context
5. Update `docs/templates/PRD-TEMPLATE.md` with your codebase paths and patterns

### Starting From Zero

The full journey from idea to feature looks like this:

```
/bootstrap A Telegram reminder bot using grammY and TypeScript
  → discussion → PROJECT.md filled → project scaffolded → ready

/new-feature Users can set daily reminders via /remind command
  → PRD → design → implement → test → review → PR
```

### Running a Feature Workflow

```
/new-feature Users should be able to set display preferences
```

This triggers the full pipeline:
1. **product-manager** agent creates a PRD
2. You review and approve
3. **architect** agent creates a technical design
4. You review and approve
5. **implementer** agent writes the code
6. **tester** agent validates acceptance criteria
7. **code-reviewer** agent reviews everything
8. You decide whether to create a PR

### Running a Bug Fix

```
/fix-bug Login fails when email contains a plus sign
```

### Manual Agent Delegation

You can also delegate to specific agents directly:

```
Use the product-manager agent to create a PRD for a notification system

Use the architect agent to design the caching layer

Use the code-reviewer agent to review changes on the current branch

Use the tester agent to validate acceptance criteria from PRD-notifications.md
```

---

## Documentation Hierarchy

The framework uses three configuration files, each with a distinct purpose:

| File | Scope | Who fills it |
|------|-------|-------------|
| `PROJECT.md` | Project-specific: tech stack, commands, directory layout, conventions | User (or `/bootstrap`) |
| `AGENTS.md` | Universal rules: code style, testing, security, git workflow | Stays as-is across projects |
| `CLAUDE.md` | Claude-specific: agent team, skills catalog, boundaries, context management | Stays as-is (extend with learnings via `/retro`) |

**PROJECT.md** is the only file you must customize per project. The `/bootstrap` skill
fills it in automatically based on your answers. If you prefer manual setup, fill in
every placeholder before running workflows.

---

## Skills Overview

35 skills organized by category. Use `/skill-name` to invoke workflow skills. Domain
skills auto-load when Claude detects relevant code.

### Workflow Skills (27)

| Category | Skill | Description |
|----------|-------|-------------|
| **Core** | `/bootstrap` | Initialize a new project from scratch |
| | `/new-feature` | Full feature pipeline: PRD → design → implement → test → review |
| | `/fix-bug` | Bug investigation → fix → regression test → review |
| | `/review-code` | Code review on current changes |
| | `/discuss` | Capture implementation preferences before design |
| | `/quick` | Fast implementation (skips PRD/design) |
| | `/refactor` | Multi-phase refactoring with incremental validation |
| | `/release` | Release notes, changelog, version bump |
| **Plan/Execute** | `/plan` | Create detailed implementation plan |
| | `/execute` | Implement from a plan file, task by task |
| | `/prime` | Load full project context |
| | `/commit` | Atomic commit with conventional prefix |
| **Validation** | `/validate` | Full health check (lint, types, tests, build) |
| | `/execution-report` | Post-implementation divergence report |
| | `/system-review` | Meta-analysis: plan vs. execution |
| | `/verify` | Map acceptance criteria to evidence |
| | `/retro` | Post-implementation retrospective |
| **Testing/Security** | `/e2e-test` | End-to-end integration tests |
| | `/security-audit` | OWASP Top 10, deps, auth review |
| **Maintenance** | `/update-deps` | Dependency updates with security audit |
| | `/perf` | Performance profiling and optimization |
| | `/migrate` | Database/API migration with rollback plan |
| | `/tech-debt` | Identify and address technical debt |
| **Session** | `/pause` | Save work context for session continuity |
| | `/resume` | Restore context and continue |
| **Docs/Investigation** | `/onboard` | Generate onboarding docs from codebase |
| | `/rca` | Root cause analysis for GitHub issues |

### Domain Skills (8)

Auto-loaded by Claude when working with relevant code. Not invoked directly.

| Skill | Covers |
|-------|--------|
| `react-patterns` | Components, hooks, state, accessibility |
| `nextjs-conventions` | App Router, Server/Client Components, data fetching |
| `node-backend` | Middleware, error handling, validation, async |
| `api-design` | REST conventions, response formats, pagination |
| `database-patterns` | Schema design, migrations, query optimization |
| `frontend-testing` | React Testing Library, component tests, MSW |
| `backend-testing` | API tests, database setup/teardown, fixtures |
| `auth-patterns` | JWT, sessions, RBAC, password hashing, CSRF |

