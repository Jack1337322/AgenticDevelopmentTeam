# PRD: [Feature Name]

**Status**: Draft | In Review | Approved | In Progress | Complete
**Author**: [name]
**Created**: [date]
**Priority**: P0 (critical) | P1 (high) | P2 (medium) | P3 (low)

---

## 1. Objective

[1-2 sentences: What are we building and why? What user problem does it solve?]

## 2. Background

[Brief context: current state, motivation, relevant decisions. 2-3 sentences.]

## 3. User Stories

### US-1: [Imperative Title]

**As a** [persona]
**I want to** [action]
**So that** [benefit]

**Acceptance Criteria:**

```
GIVEN [precondition]
WHEN [action]
THEN [expected result]
AND [additional assertion]
```

```
GIVEN [precondition]
WHEN [action]
THEN [expected result]
```

**Examples:**

| Input | Expected Output |
|-------|----------------|
| `{"email": "valid@test.com"}` | `{"status": 201, "id": "usr_xxx"}` |
| `{"email": ""}` | `{"status": 400, "error": "Email required"}` |

**Complexity**: S | M | L
**Dependencies**: None

---

### US-2: [Imperative Title]

**As a** [persona]
**I want to** [action]
**So that** [benefit]

**Acceptance Criteria:**

```
GIVEN [precondition]
WHEN [action]
THEN [expected result]
```

**Complexity**: S | M | L
**Dependencies**: US-1

---

## 4. Technical Context

### Relevant Files

| File | Purpose |
|------|---------|
| `src/services/[relevant].ts` | Service to extend |
| `src/models/[relevant].ts` | Data model to modify |
| `src/api/routes/[relevant].ts` | API routes |
| `tests/[relevant].test.ts` | Existing test patterns |

### Existing Patterns to Follow

```typescript
// Example from codebase showing the pattern agents should replicate
// (paste a real code snippet here)
```

### Data Model Changes

```sql
-- Describe any schema changes
-- ALTER TABLE ... ADD COLUMN ...
-- CREATE TABLE ...
```

### API Changes

```
METHOD /api/v1/endpoint
  Request:  { field: type }
  Response: { field: type }
  Errors:   400 (validation), 401 (unauthorized), 404 (not found)
```

## 5. Non-Functional Requirements

| Requirement | Target | How to Validate |
|-------------|--------|----------------|
| API latency | < 200ms p95 | Load test |
| Test coverage | > 80% new code | `pnpm test:coverage` |
| Accessibility | WCAG 2.1 AA | Axe audit |

## 6. Implementation Phases

### Phase 1: Data Layer

1. Create migration: `src/db/migrations/XXX_[name].ts`
2. Update model: `src/models/[name].ts`
3. Add repository method: `src/repositories/[name].ts`
4. Write tests: `tests/repositories/[name].test.ts`

**Validation**: `pnpm test -- tests/repositories/[name]`

### Phase 2: Service Layer

1. Add service method: `src/services/[name].ts`
2. Add validation schema: `src/schemas/[name].ts`
3. Write tests: `tests/services/[name].test.ts`

**Validation**: `pnpm test -- tests/services/[name]`

### Phase 3: API Layer

1. Add route: `src/api/routes/[name].ts`
2. Write integration tests: `tests/integration/[name].test.ts`

**Validation**: `pnpm test -- tests/integration/[name]`

### Phase 4: UI (if applicable)

1. Add component: `src/ui/components/[Name].tsx`
2. Add hook: `src/ui/hooks/use[Name].ts`
3. Write tests: `src/ui/components/[Name].test.tsx`

**Validation**: `pnpm test -- src/ui/components/[Name]`

## 7. Out of Scope

- [Explicitly list what this PRD does NOT cover]
- [Prevents scope creep during implementation]

## 8. Boundaries

### ALWAYS (agent can do freely)
- Run tests, linters, type checks
- Create/edit files within scope of this feature
- Follow patterns from existing codebase

### ASK FIRST (requires human approval)
- Add new npm dependencies
- Modify database schemas beyond what's specified above
- Change shared interfaces

### NEVER
- Modify existing migration files
- Commit secrets or credentials
- Skip writing tests
- Use `any` type

## 9. Risks & Mitigations

| Risk | Impact | Mitigation |
|------|--------|-----------|
| [What could go wrong] | High/Med/Low | [Strategy] |

## 10. Validation Checklist

- [ ] All acceptance criteria have passing tests
- [ ] `pnpm test` passes
- [ ] `pnpm typecheck` passes
- [ ] `pnpm lint` passes
- [ ] No `any` types introduced
- [ ] No secrets in code
- [ ] Migration is reversible
