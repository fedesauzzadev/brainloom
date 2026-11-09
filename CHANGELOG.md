# Changelog

All notable changes to this project are documented here.
Format: [Keep a Changelog](https://keepachangelog.com/en/1.1.0/); versioning: [SemVer](https://semver.org/).
Entries that change the brain format, config, or skill contracts are marked **[BREAKING]**.

## [Unreleased]

### Added
- Core brain templates (`schema_version: 1`): index, vision, roadmap, conventions, shared registry, node, decision, config.
- Skills: `triage` (impact-radius classification and routing), `memory-update` (closing the loop: nothing is done until the brain reflects it).
- `AGENTS.md` instance template.
- Repo skeleton: `/core` (tool-agnostic), `/adapters/opencode`, `/scripts`, `/tests`.
- OpenCode adapter: global installer with collision guard (`adapters/opencode/install.mjs`), session-notice plugin (update notice on first prompt, opt-out, offline-tolerant).
- Skills: `init-brain` (onboarding: discover, ask, generate, validate), `kit-update` (changelog + confirm + update + migrate).
- Skills: `plan-project` (whole idea → ordered vertical slices, shared candidates, risks; records roadmap after approval) and `build-slice` (decompose into nodes, acceptance criteria first, thin end-to-end, functional verification, close the slice).
- Skills: `verify` (criteria audit, tests, functional execution, independent refutation) and `small-change` (encapsulated FIX/S flow).
- OpenCode agent `brainloom/verifier`: independent read-only subagent with a refutation mandate (edits denied, execution allowed).
- `/fix` command (triage → small-change).
- `/kit-update` command.
- Scripts: `check-update`, `validate-brain`, `migrate` (dry-run default, backup, validation, rollback).
- Migrations skeleton + rules (`core/migrations/`), test fixtures for validation and the update/migration drill.
- CI: cross-OS (ubuntu/macos/windows) syntax check, brain validation, migration dry-run, offline tolerance.
