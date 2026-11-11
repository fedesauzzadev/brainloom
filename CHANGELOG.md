# Changelog

All notable changes to this project are documented here.
Format: [Keep a Changelog](https://keepachangelog.com/en/1.1.0/); versioning: [SemVer](https://semver.org/).
Entries that change the brain format, config, or skill contracts are marked **[BREAKING]**.

## [Unreleased]

## [0.4.1] - 2026-11-10

### Fixed
- `check-update` serving a cache entry written by the session-notice plugin printed `up to date (?)` / `? -> undefined available` — the plugin cached `{update, line}` without explicit versions. The script now falls back to the cached `line`, and the plugin records `local`/`remote` in new cache entries.
- `core/migrations/README.md` referenced a CONTRIBUTING file that does not exist; it now points at the rules in the same document.

## [0.4.0] - 2026-11-10

### Added
- `scripts/smoke.mjs` — kit self-check + skill verification runner. Structural mode (CI, offline): every skill declares a `## Verification` contract, referenced fixtures exist and their brains stay valid, every shipped `.mjs` parses, and any `.ps1`/`.cmd`/`.bat` is ASCII-only or UTF-8 with BOM. `--agent` mode runs each contract's task through the harness (`opencode run`) on a throwaway fixture copy and asserts expected artifacts (`file` / `grep` / `valid` ops) — verifying a skill no longer costs a full session.
- Every core skill ships a `## Verification` section (fixture, task, observable asserts). `triage`, `memory-update` and `init-brain` are agent-runnable contracts; `kit-update` declares its manual drill.
- Node frontmatter `verification.level` (`smoke` | `full`): declared depth of verification. `full` = tests + functional run (default for product code); `smoke` = structure validated, behavior spot-checked — only for orchestration/spec deltas. Additive optional field, no schema bump (same policy as `verify:` in 0.3.0).
- `init-brain` non-interactive mode (§2b) for orchestrators: documented defaults, every assumption recorded as a reversible decision, then generate-validate-report. No more hand-rolled bypasses.
- `brain/conventions.md` template: file-ownership table — one writer per file, extended by multi-role orchestrators before raising `max_parallel_agents`.
- Windows script rule (ASCII-only or BOM for `.ps1`/`.cmd`/`.bat`) in `scripts/README.md` and `adapters/opencode/README.md`, enforced by `smoke.mjs`: PS 5.1 reads BOM-less UTF-8 as ANSI.
- `tests/fixtures/empty-project` for the init-brain contract.
- `tests/fake-agent.mjs` + CI step: the `--agent` plumbing (copy fixture → run → assert artifacts) is exercised offline on every push, no LLM needed.

### Changed
- `validate-brain` rejects invalid `verification.level` values (error) and warns when `verified`/`shipped` nodes declare no level — the smoke-vs-full gray zone is now visible instead of implicit.
- Installer: bootstrap installs (run from a temp copy without `.git`) record a self-contained kit snapshot under `<config>/brainloom-kit/` instead of a `kit_path` that dangles after the temp dir is deleted. Manifest gains `source: clone | snapshot`; re-installing from a real clone cleans the stale snapshot up. `kit-update` explains the clone requirement on snapshot installs.

## [0.3.0] - 2026-11-09

### Removed
- `core/migrations/0001-rename-verification-to-proof`: drill fiction committed into the real migrations dir — no template or skill ever spoke `proof:`. The drill fixture survives in `tests/fixtures/migrations/` (CI-only), where it belongs.

### Changed
- **[BREAKING]** Node `status` vocabulary: `done` is removed; `implemented` and `shipped` join the enum (`planned | in-progress | implemented | verified | shipped | superseded`). `verified` = agent-done and requires a filled `verification` block; `shipped` = human gates (commit/deploy/merge). Migration `0001-rename-done-to-shipped` upgrades brains (schema 1 → 2): `done` with evidence → `shipped`, `done`/`verified` without evidence → demoted to `implemented`. Core templates now ship `schema_version: 2`.
- `validate-brain` rejects `verified`/`shipped` with empty verification fields and warns when they lack a `verify` recipe. Pre-schema-2 `done` nodes validate as legacy warnings (migration `0001` rewrites or demotes them), so mid-chain runner validation cannot deadlock.

### Added
- Node frontmatter `verify:` field — the exact command sequence to re-verify a node's contract, written on first verification of an area so the next one is a single read.
- `memory-update` skill: explicit status ladder, the "no evidence → ceiling is `implemented`" rule, gates-never-block-local-verification rule, and first-verification recipe writing.
- `AGENTS.md` template: agent-done vs shipped distinction under "Done means".

## [0.2.0] - 2026-11-09

### Changed
- Drill (test-only, no brain format change): simulated BREAKING migration fixture `rename-verification-to-proof` for the update/migration flow; lives under `tests/fixtures/migrations/`.

### Added
- Core brain templates (`schema_version: 1`): index, vision, roadmap, conventions, shared registry, node, decision, config.
- Skills: `triage` (impact-radius classification and routing), `memory-update` (closing the loop: nothing is done until the brain reflects it).
- `AGENTS.md` instance template.
- Repo skeleton: `/core` (tool-agnostic), `/adapters/opencode`, `/scripts`, `/tests`.
- OpenCode adapter: global installer with collision guard (`adapters/opencode/install.mjs`), session-notice plugin (update notice on first prompt, opt-out, offline-tolerant).
- Skills: `init-brain` (onboarding: discover, ask, generate, validate), `kit-update` (changelog + confirm + update + migrate).
- `/kit-update` command.
- Scripts: `check-update`, `validate-brain`, `migrate` (dry-run default, backup, validation, rollback).
- Migrations skeleton + rules (`core/migrations/`), test fixtures for validation and the update/migration drill.
- CI: cross-OS (ubuntu/macos/windows) syntax check, brain validation, migration dry-run, offline tolerance.
