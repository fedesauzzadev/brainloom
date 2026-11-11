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
- PASS → agent-done: node `status: verified` with the `verification` block
  filled and `level` declared in the same edit (`full` for product code;
  `smoke` only for orchestration/spec deltas).
- FAIL or partial → report its findings verbatim; the node stays
  `implemented` (the claim did not hold). Fix, then re-verify.

## 5. What cannot be verified
State explicitly anything unverifiable (no harness, environment limits) and its
risk. Never declare done over an unverified gap.

## 6. Close
Update node (`verification` fields incl. `level`, `status: verified`), evidence
file, `brain/index.md`. Human gates (commit, deploy, merge) later promote it
to `shipped`.

## Verification
Fixture: tests/fixtures/sample-project
Task: Node N-0001 claims its acceptance criterion (node app.js prints a greeting) is implemented. Run the verify skill on N-0001 end-to-end, including the independent verifier subagent.
- [ ] Criteria audit, functional run, and refutation all executed — status only climbs with evidence
- [ ] N-0001 lands agent-done: verified + verification block + level + evidence file
- [ ] Index reflects the new status

expect: grep brain/nodes/N-0001.md "status: verified"
expect: grep brain/nodes/N-0001.md "level: full"
expect: file brain/evidence/N-0001.md
expect: valid brain
