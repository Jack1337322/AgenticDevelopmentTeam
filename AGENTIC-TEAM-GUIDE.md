# Agentic Product Development Team -- Setup Guide & Research

> Enterprise-grade agentic development workflow using Claude Code sub-agents.
> Researched February 2026.

---

## What This Is

A complete, ready-to-use setup for running an AI-powered product development team
using Claude Code. The team consists of specialized agents (product manager, architect,
developer, tester, reviewer, debugger, docs writer) that collaborate through a
defined workflow to go from feature idea to merged PR.

## Files Created

```
AgenticDevelopmentTeam/
├── CLAUDE.md                              # Claude-specific project context
├── AGENTS.md                              # Universal agent instructions (all AI tools)
├── AGENTIC-TEAM-GUIDE.md                  # This file -- guide + research
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
│   └── commands/
│       ├── new-feature.md                 # /new-feature [description]
│       ├── fix-bug.md                     # /fix-bug [description]
│       └── review-code.md                 # /review-code
└── docs/
    ├── templates/
    │   └── PRD-TEMPLATE.md                # Agent-optimized PRD template
    ├── prds/                              # Generated PRDs go here
    └── architecture/                      # Design documents go here
```

---

## How to Use

### Quick Start

1. Copy this directory structure into your project
2. Fill in `PROJECT.md` with your tech stack, commands, directory layout, and conventions
3. Update `.claude/settings.json` with Bash permissions for your project's tools (see `PROJECT.md` Permissions Guidance)
4. Customize `CLAUDE.md` with any additional project context
5. Update `docs/templates/PRD-TEMPLATE.md` with your codebase paths and patterns

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

## Research: Enterprise Agentic Development Landscape (2026)

### Leading Frameworks

| Framework | By | Architecture | Best For |
|-----------|-----|-------------|----------|
| **Claude Agent SDK** | Anthropic | Same tools as Claude Code | Code-centric dev teams |
| **LangGraph 1.0** | LangChain | Graph-based, durable execution | Complex conditional workflows |
| **OpenAI Agents SDK** | OpenAI | Handoffs + agents-as-tools | OpenAI ecosystem |
| **Microsoft Agent Framework** | Microsoft | AutoGen + Semantic Kernel merged | Azure / enterprise |
| **Google ADK** | Google | Hierarchical agent composition | Google Cloud / Vertex AI |
| **AWS Strands Agents** | AWS | Model-driven, minimal code | AWS Bedrock |
| **CrewAI** | CrewAI | Role-based crews | Team simulation |
| **MetaGPT** | DeepWisdom | Full company simulation (5 roles) | End-to-end code generation |

### Interoperability Protocols

| Protocol | Purpose | Status |
|----------|---------|--------|
| **MCP** (Model Context Protocol) | Agent-to-tool communication | Production. 10,000+ servers. Linux Foundation. |
| **A2A** (Agent-to-Agent) | Peer-to-peer agent coordination | Production. 50+ partners. Linux Foundation. |
| **AGENTS.md** | Cross-platform project instructions | 60,000+ projects. 25+ coding agents. |
| **ACP** (Agent Communication Protocol) | Lightweight REST messaging | IBM BeeAI. Linux Foundation. |

### Industry Statistics

| Metric | Value |
|--------|-------|
| Developers using AI tools daily | 51% |
| Code that is AI-generated | 41% |
| Enterprises using/testing AI agents | 72% |
| AI agent investment increasing | 84% of leaders |
| Organizations with agents in production | 11% |
| Multi-agent vs single-agent performance | +90% (Anthropic benchmark) |
| AI-generated code vulnerability rate | 2.74x higher than human (Veracode) |

### Google's 8 Multi-Agent Design Patterns

1. **Sequential Pipeline** -- Assembly line, each agent passes output forward
2. **Coordinator/Dispatcher** -- Central agent routes to specialists
3. **Parallel Fan-Out/Gather** -- Simultaneous execution, outputs aggregated
4. **Hierarchical Decomposition** -- Break goals into subtasks recursively
5. **Generator and Critic** -- One creates, another validates
6. **Iterative Refinement** -- Progressive enhancement through critique loops
7. **Human in the Loop** -- Pause for human review at critical points
8. **Composite** -- Combine patterns for complex systems

**This setup primarily uses patterns 1 (Sequential Pipeline), 2 (Coordinator/Dispatcher),
and 7 (Human in the Loop).**

### What Makes PRDs Agent-Executable

Based on research across Chief, Ralph, ProdMoh, context-engineering-intro, and PRPs-agentic-eng:

1. **Testable acceptance criteria** -- GIVEN/WHEN/THEN predicates, not prose
2. **Explicit file paths** -- tell agents exactly where to look and where to write
3. **Code examples** -- show existing patterns agents should follow
4. **Validation commands** -- runnable commands after each phase
5. **Single-session scope** -- each story completable in one context window
6. **Dependency ordering** -- explicit phases with blocking relationships
7. **Three-tier boundaries** -- ALWAYS/ASK FIRST/NEVER

### The Verification Lattice (Quality Gates)

```
Layer 1: DETERMINISTIC   -- build, unit tests, lint, typecheck
Layer 2: SEMANTIC         -- contract tests, golden tests, snapshots
Layer 3: SECURITY         -- SAST, dependency scan, secret scan
Layer 4: AGENTIC          -- code-reviewer agent for style + spec adherence
Layer 5: HUMAN            -- escalations and final acceptance
```

### Human-in-the-Loop: When Humans Must Intervene

- Requirements are ambiguous or acceptance criteria are missing
- Architectural decisions affect multiple services
- New external dependencies are being introduced
- Tests fail with unclear root cause
- Security-sensitive changes (auth, crypto, payments)
- High blast-radius changes (shared interfaces, database schemas)

### Key Case Studies

| Company | What | Result |
|---------|------|--------|
| **Anthropic** | 16 parallel Claude agents built a C compiler | 100K lines, compiles Linux kernel, ~$20K cost |
| **Zapier** | 800+ internal agents | 89% AI adoption company-wide |
| **TELUS** | Agentic coding across org | 30% faster delivery, 500K+ hours saved |
| **Rakuten** | Claude Code on 12.5M-line codebase | 7-hour complex implementation, 99.9% accuracy |
| **Mercedes-Benz FS** | Multi-agent CRM | 20% new business growth, 15% cross-sell boost |

### Anti-Patterns to Avoid

1. **Making everything agentic** -- Use agents for ambiguous tasks, rules for deterministic ones
2. **Overloading context windows** -- Scope precisely, use just-in-time context loading
3. **Agent-introduced pattern rot** -- Enforce architectural linting and golden path templates
4. **Skipping observability** -- Instrument from day one; log every decision and tool call
5. **Scaling before governing** -- Never add agents faster than your monitoring can keep up

---

## Claude Code Sub-Agent Reference

### YAML Frontmatter Fields

| Field | Type | Values | Description |
|-------|------|--------|-------------|
| `name` | string | `lowercase-hyphens` | Unique agent identifier |
| `description` | string | free text | When Claude should use this agent |
| `tools` | string | comma-separated | Allowed tools (Read, Write, Edit, Bash, Glob, Grep, WebSearch, etc.) |
| `disallowedTools` | string | comma-separated | Denied tools |
| `model` | string | `opus`, `sonnet`, `haiku`, `inherit` | Model selection |
| `permissionMode` | string | `default`, `acceptEdits`, `dontAsk`, `bypassPermissions`, `plan` | Permission handling |
| `maxTurns` | int | positive integer | Max agentic turns |
| `memory` | string | `user`, `project`, `local` | Persistent memory scope |
| `background` | bool | `true`/`false` | Run as background task |
| `isolation` | string | `worktree` | Run in isolated git worktree |
| `skills` | list | skill names | Skills injected at startup |
| `mcpServers` | map | server configs | MCP servers for this agent |
| `hooks` | map | hook configs | Lifecycle hooks |

### Permission Modes Explained

| Mode | Behavior |
|------|----------|
| `plan` | Read-only. Agent can research and plan but not modify files. |
| `default` | Asks for permission on every write/execute action. |
| `acceptEdits` | Auto-approves file edits. Asks for Bash commands. |
| `dontAsk` | Auto-approves edits + Bash commands matching allowlist. |
| `bypassPermissions` | Auto-approves everything. Use with caution. |

### Agent Teams (Experimental)

Enable in settings:
```json
{"env": {"CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS": "1"}}
```

Agent teams allow multiple Claude Code instances to work in parallel:
- **Team Lead**: coordinates work, spawns teammates
- **Teammates**: independent context windows, claim tasks from shared list
- **Task List**: shared with pending/in_progress/completed states and dependencies
- **Mailbox**: direct inter-agent messaging

Best for: parallel implementation of independent modules, concurrent research,
competing approaches to the same problem.

---

## Sources

### Anthropic / Claude Code
- [Claude Code Sub-Agents](https://code.claude.com/docs/en/sub-agents)
- [Claude Code Agent Teams](https://code.claude.com/docs/en/agent-teams)
- [Claude Code Best Practices](https://code.claude.com/docs/en/best-practices)
- [Using CLAUDE.md Files](https://claude.com/blog/using-claude-md-files)
- [Claude Agent SDK](https://platform.claude.com/docs/en/agent-sdk/overview)
- [Building a C Compiler with Parallel Claudes](https://www.anthropic.com/engineering/building-c-compiler)
- [2026 Agentic Coding Trends Report](https://resources.anthropic.com/2026-agentic-coding-trends-report)

### Standards & Protocols
- [AGENTS.md Specification](https://agents.md/)
- [Model Context Protocol (MCP)](https://modelcontextprotocol.io/specification/2025-11-25)
- [Agent-to-Agent Protocol (A2A)](https://developers.googleblog.com/en/a2a-a-new-era-of-agent-interoperability/)

### Frameworks
- [LangGraph 1.0](https://changelog.langchain.com/announcements/langgraph-1-0-is-now-generally-available)
- [Microsoft Agent Framework](https://learn.microsoft.com/en-us/agent-framework/overview/agent-framework-overview)
- [Google ADK](https://google.github.io/adk-docs/)
- [OpenAI Agents SDK](https://openai.github.io/openai-agents-python/)
- [AWS Strands Agents](https://strandsagents.com/latest/)
- [CrewAI](https://docs.crewai.com/)
- [MetaGPT](https://docs.deepwisdom.ai/main/en/guide/get_started/introduction.html)

### PRD Templates & Methodology
- [Addy Osmani: Good Specs for AI Agents](https://addyosmani.com/blog/good-spec/)
- [ProdMoh: Agentic PRD](https://prodmoh.com/blog/agentic-prd)
- [context-engineering-intro](https://github.com/coleam00/context-engineering-intro)
- [PRPs-agentic-eng](https://github.com/Wirasm/PRPs-agentic-eng)
- [PRD-driven-context-engineering](https://github.com/mattgierhart/PRD-driven-context-engineering)
- [Chief PRD Format](https://minicodemonkey.github.io/chief/concepts/prd-format.html)
- [Ralph Autonomous Agent](https://github.com/snarktank/ralph)

### Industry Research
- [Google: 8 Multi-Agent Design Patterns](https://www.infoq.com/news/2026/01/multi-agent-design-patterns/)
- [LangChain: Multi-Agent Architecture](https://blog.langchain.com/choosing-the-right-multi-agent-architecture/)
- [Deloitte Tech Trends 2026](https://www.deloitte.com/us/en/insights/topics/technology-management/tech-trends/2026/agentic-ai-strategy.html)
- [Veracode: AI Code Security](https://www.veracode.com/blog/securing-code-and-agentic-ai-risk/)
- [Zapier AI Agents Survey 2026](https://zapier.com/blog/ai-agents-survey/)
