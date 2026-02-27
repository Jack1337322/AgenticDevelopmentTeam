---
description: Create an atomic commit for current changes
---

# Commit Current Changes

Run `git status` and `git diff HEAD` to see all uncommitted changes.

Stage the relevant untracked and changed files.

Create an atomic commit with a conventional commit message:

- Use a prefix: `feat:`, `fix:`, `docs:`, `chore:`, `refactor:`, `test:`, `style:`, `perf:`
- Write a concise message describing the change
- If there are multiple logical changes, suggest separate commits

Do NOT push to remote unless explicitly asked.
