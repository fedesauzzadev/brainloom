---
name: Brainloom Verify
description: Real verification of a task or node — acceptance-criteria audit, tests, functional execution, and an independent read-only verifier subagent whose job is to REFUTE that it works. Use when a node reaches verification, when the user asks to verify or check work, or before marking anything done.
---

# Verify

"Done" is earned here. Nothing is verified by having been written.

## 1. Acceptance criteria audit
Every `acceptance_criteria` entry of the node: met and observable, or explicitly
marked unmet with a reason. No silent drops, no reinterpretation.

## 2. Tests
Run `commands.test` from `brain/config.yaml`. No harness? Say so and lean on
step 3 — do not pretend tests exist.

## 3. Functional verification
Actually run the thing (`commands.run`, CLI, endpoint, flow) per criterion.
Expected vs observed, each step. Save a short evidence file in
`brain/evidence/` and reference it from the node.

## 4. Independent verification (refutation)
Spawn the read-only verifier subagent (harness namespace, e.g.
`brainloom/verifier`). Resolve its model level (`balanced` or `strong`) from
`models` in `brain/config.yaml` — never hardcode a model. Give it:
- the node id(s) and their acceptance criteria,
- what was built and the claimed evidence,
- how to run the thing (commands from config),
and the mandate: TRY TO REFUTE. It executes but does not edit production code.
- PASS → node `status: done`.
- FAIL or partial → report its findings verbatim; node stays `verified` at
  best. Fix, then re-verify.

## 5. What cannot be verified
State explicitly anything unverifiable (no harness, environment limits) and its
risk. Never declare done over an unverified gap.

## 6. Close
Update node (`verification` fields, `status`), evidence file, `brain/index.md`.
