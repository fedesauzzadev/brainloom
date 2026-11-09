---
name: Brainloom Small Change
description: Encapsulated FIX/S workflow for small fixes and tweaks on top of existing work — 0-1 nodes affected, no shared contracts, localizable cause. Use when triage classifies a task as FIX/S, or for a bug fix, copy change, or small adjustment that does not touch contracts.
---

# Small Change (FIX/S)

Triage already classified this FIX/S. Keep it small and encapsulated.

## 1. Locate
- Read the affected node(s) (`affects` links) and ONLY the code they point to.
- Confirm the cause is local. If it spreads (contracts, several nodes), STOP —
  re-classify via `triage`: it is M or L, not S.

## 2. Acceptance criteria first
One node (`size: S`, `type: fix`), acceptance criteria as observable behavior
BEFORE the change. Fold into an existing node only if it is literally the same
defect.

## 3. Fix encapsulated
- The minimum diff that satisfies the criteria. No drive-by refactors, no
  renames, no "while I'm here".
- Reuse existing helpers; add no abstractions.
- Stay within `limits` from `brain/config.yaml` — an S beyond limits is not an S.

## 4. Verify (see the verify skill)
Tests (`commands.test`) + functional run per criterion + independent verifier
for `done`. Evidence in `brain/evidence/`.

## 5. Close
`memory-update`: node verification + status, `affects` links, index. New
duplication candidate? Registry — still no abstraction before three uses.
