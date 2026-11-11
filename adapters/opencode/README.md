# adapters/opencode

OpenCode adapter: global installer, session-notice plugin, agent definitions,
commands. Ships in Slice 2+. Content lives in `/core`; this adapter only
places it where OpenCode expects it (`~/.config/opencode/`).

Windows rule: any `.ps1`/`.cmd`/`.bat` added here must be ASCII-only or UTF-8
with BOM (see `scripts/README.md`). Prefer plain Node `.mjs`.

The installer records the kit origin in the manifest
(`~/.config/opencode/brainloom.kit.json`): `source: clone` (git-pullable) or
`source: snapshot` (bootstrap install from a temp copy — self-contained under
`~/.config/opencode/brainloom-kit/`; git-based updates then require
re-installing from a clone).
