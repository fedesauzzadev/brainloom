---
name: Brainloom Init Brain
description: Onboard a project into brainloom — generate the brain/ memory graph, stamp config.yaml with the project's real commands, model mapping and language, and create or extend AGENTS.md. Use when the user wants to start using brainloom in a project, or when a brainloom skill runs and brain/ does not exist.
---

# Init Brain (onboarding)

Runs in the USER's project. Assume nothing about their setup: discover first,
then ask. Never assume the kit author's environment.

## 0. Preconditions
- Node present? Run `node --version`. If missing: warn that kit scripts
  (check-update, validate-brain, migrate) will not work; continue anyway.
- Kit location: read the manifest at `~/.config/opencode/brainloom.kit.json`
  (written by the installer) → `kit_path`. If absent, ask for the kit clone path.

## 1. Discover (before asking)
- New or existing project? (existing = has source code or a dependencies file)
- If EXISTING: confirm scope — full `adopt` mapping (recommended) or an empty
  brain that grows organically.
- Detect commands from build files: package.json scripts, Makefile,
  pyproject.toml, Cargo.toml, go.mod, etc. Propose detected values as recommendations.
- Language for brain files: ask (default: the user's own language).

## 2. Ask (once, numbered, with recommendations)
Only what discovery could not answer: commands test/lint/build/run, the
strong/balanced/fast model mapping (list available models if your harness
provides a way, e.g. `opencode models`), and the update `remote_url`
(default: the kit clone's git origin URL).

## 2b. Non-interactive mode (orchestrators)
When invoked inside an automated flow and no user is available (the caller
says non-interactive, headless, or --yes): skip §2 entirely. Discover
everything you can (§1), apply documented defaults for the rest (commands
detected or empty, models empty, `remote_url` = the kit clone's origin),
record EVERY assumption as one short decision in `brain/decisions/`
(reversible — surfaced in the report), then generate (§3), validate (§4),
and report (§5). A wrong assumption recorded as a decision is fixable; a
blocked pipeline is not. Never guess silently.

## 3. Generate
- Copy `<kit_path>/core/templates/brain/*` → `<project>/brain/`
  (keep `_template.md` and `.gitkeep`).
- Stamp `brain/config.yaml`: `kit_version` from the kit's `VERSION` file,
  `language`, `commands`, `models`, `remote_url`.
- `AGENTS.md`: create from `<kit_path>/core/templates/AGENTS.md`. If one
  exists, append ONLY the marked brainloom block — never rewrite user content.

## 4. Validate
Run `node <kit_path>/scripts/validate-brain.mjs <project>/brain` — must pass.

## 5. Report
What was generated, what was asked vs assumed (assumptions are reversible —
say so), and the next step: `triage` the first task; for existing projects, `adopt`.

## Verification
Fixture: tests/fixtures/empty-project
Task: Run init-brain in non-interactive mode on this project — no questions, documented defaults, every assumption recorded as a decision.
- [ ] Creates brain/ from the kit templates and a stamped brain/config.yaml
- [ ] brain/config.yaml carries schema_version: 2 and the detected commands
- [ ] Creates/appends AGENTS.md and the assumptions land in brain/decisions/
- [ ] validate-brain passes on the generated brain

expect: file brain/config.yaml
expect: grep brain/config.yaml "schema_version: 2"
expect: grep brain/config.yaml "test:"
expect: file AGENTS.md
expect: file brain/decisions
expect: valid brain
