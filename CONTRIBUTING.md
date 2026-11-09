# Contributing

Small, verified changes. Follow the slices in the repo's own brain if one is
active; otherwise keep PRs minimal and scoped.

## Ground rules

- **Skills** live in `core/skills/`, in English, ≤ ~120 lines each, with a
  precise `description` (it drives auto-discovery).
- **Scripts** in `/scripts`: Node.js, standard library only, no dependencies,
  cross-platform (Windows / macOS / Linux). Mind line endings (the repo
  enforces LF via `.gitattributes`).
- **No coupling**: `/core` must never reference a specific harness. Harness
  specifics (paths, agent formats) belong in `adapters/<tool>/`.
- **No personal data** in the repo: no absolute paths, no user names, no model
  IDs, no keys. The kit is public; instances are private.

## The golden rule (format changes)

> If you change a brain/config FORMAT, you bump `schema_version`, you write
> the migration, and you mark the changelog entry **[BREAKING]**. All three,
> in the same change.

- Migrations live in `core/migrations/NNNN-description/` (`NNNN` = the schema
  it starts from): a `README.md` + `migrate.mjs` exporting
  `migrate({ brainDir, dryRun })`. Idempotent, dry-run safe, throws on failure
  (the runner backs up and rolls back). See `core/migrations/README.md`.
- Skill/agent/command-only changes need NO migration and NO schema bump.

## Before you push

- `node scripts/validate-brain.mjs tests/fixtures/sample-project/brain` passes.
- `node scripts/migrate.mjs tests/fixtures/sample-project/brain --migrations-dir tests/fixtures/migrations` (dry-run) prints the plan cleanly.
- CI (ubuntu/macos/windows) is green.
- If you touched a format: the migration drill (dry-run → apply → validate →
  forced-failure rollback) was run against a copy of a real brain.
