---
name: Brainloom Memory Update
description: Update the project brain after finishing work — node status, verification fields, code pointers, index, registry candidates, and decisions. Use when a task, fix, or slice was completed or changed status; nothing is done until the brain reflects it.
---

# Memory Update

The code is the source of truth; the brain is a map with pointers. This skill
is the closing step of any task. No node update → not done.

## 1. Update the node
- `status`: `in-progress` → `verified` only with evidence; `done` after
  independent verification. `superseded` when replaced (keep the link).
- Fill `verification`: tests run (+ result), functional check performed
  (+ result), evidence path.
- Fill or refresh `code` pointers as `path/file.ext -> symbol`. Pointers, never copies.
- Update `decisions`, `affects`, `replaces`, `contracts_touched` if they changed.

## 2. Acceptance criteria audit
Every `acceptance_criteria` entry must be met-and-observable, or explicitly
marked unmet with a reason. No silent drops, no silent scope changes.

## 3. Evidence
Write one short file per verification under `brain/evidence/`: what ran,
expected vs observed, date. Reference it from the node's `verification.evidence`.

## 4. Registry
- Spotted a duplication candidate (2nd occurrence)? Add it to
  `brain/shared/registry.md` under Candidates. Do NOT abstract yet —
  rule of three: abstract on the 3rd occurrence, promoted from Candidates.
- Before writing anything new: consult `registry.md` and `brain/conventions.md`
  first. If it exists, reuse it.

## 5. Index
Update `brain/index.md`: new nodes, changed statuses, changed links, current
slice. Keep it under 150 lines — if over, summarize or split.

## 6. Decisions
Any non-obvious choice or assumption made along the way? One short ADR in
`brain/decisions/` (context, decision, reversibility). Reversible assumptions
get recorded, not asked.

## 7. Keep it light
Any file past its budget (node body >40 lines, index >150 lines)? Split or
summarize it now. The brain stays a map, not a transcript.
