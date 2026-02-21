Execute the following workflow for fixing a bug. Follow each step in order.

## Step 1: Investigate
Use the **debugger** agent to investigate the root cause of this bug.

## Step 2: Human Review
Present the investigation findings including:
- Root cause
- Proposed fix
- Confidence level
- Regression risk

Wait for my approval before proceeding.

## Step 3: Fix
Create a branch: `fix/[bug-description]`
Use the **implementer** agent to apply the approved fix.

## Step 4: Test
Use the **tester** agent to:
- Verify the bug is fixed
- Add a regression test that would catch this bug
- Run the full test suite

## Step 5: Review
Use the **code-reviewer** agent to review the fix.

## Step 6: Summary
Present results and ask if I want to create a PR.

---

Bug: $ARGUMENTS
