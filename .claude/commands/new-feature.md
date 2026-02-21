Execute the following workflow for a new feature. Follow each step in order.

## Step 1: Create PRD
Use the **product-manager** agent to create a PRD from this feature description.
The agent should save it to `docs/prds/PRD-[feature-name].md`.

## Step 2: Human Review
Present a summary of the PRD to me. Wait for my approval before proceeding.
If I request changes, update the PRD and present again.

## Step 3: Create Technical Design
Use the **architect** agent to create a technical design based on the approved PRD.
The agent should save it to `docs/architecture/[feature-name].md`.

## Step 4: Human Review
Present a summary of the technical design. Wait for my approval before proceeding.

## Step 5: Implement
Create a feature branch: `feat/[feature-name]`
Use the **implementer** agent to implement each phase from the design doc.
After each phase, run: `pnpm test && pnpm typecheck && pnpm lint`

## Step 6: Test
Use the **tester** agent to validate all acceptance criteria from the PRD
and write any missing tests.

## Step 7: Review
Use the **code-reviewer** agent to review all changes on the feature branch.

## Step 8: Summary
Present a final summary:
- What was implemented
- Test results and coverage
- Review findings
- Any open items

Ask me if I want to create a PR.

---

Feature: $ARGUMENTS
