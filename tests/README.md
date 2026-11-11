# tests

Example projects and migration fixtures. Populated from Slice 2 onward.

- `fixtures/sample-project` — real mini project with a brain; used by
  validate-brain, the migration dry-run, and the triage/memory-update skill
  contracts.
- `fixtures/empty-project` — no brain yet; used by the init-brain contract.
- `fixtures/migrations/` — drill migrations (CI-only, never shipped as real).
- `fake-agent.mjs` — offline stand-in for `opencode run` that applies the
  triage contract to the fixture; proves smoke.mjs `--agent` plumbing in CI
  without an LLM. Pass `--noop` to simulate an agent that did nothing.
