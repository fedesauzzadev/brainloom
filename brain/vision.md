# Vision

## What this project is
A versioned, tool-agnostic methodology kit (skills + agents + templates + scripts)
that gives AI-assisted development criterion, limits, and memory. Installed once,
used in any project. Every change to the kit is verified by commands that actually
ran — the kit is held to its own standard.

## What this project is NOT
- Not a harness, not a model, not a framework of runtime code — skills and thin
  stdlib-only scripts only.
- Not multi-harness yet: one adapter (OpenCode). Claims of portability are
  aspirational until a second adapter exists.
- Not ceremonial: small refined tasks take the Fast-Path and touch no brain state.

## Constraints
- Node stdlib only in /scripts (no dependencies), cross-platform (Windows first).
- ASCII-only or BOM'd UTF-8 for any .ps1/.cmd/.bat (PowerShell 5.1 mangles BOM-less).
- Token economy is a golden rule: agent spawns are cost-gated; chat carries
  pointers, not dumps.
- Keep-a-Changelog + SemVer; additive brain-format fields need no schema bump.
