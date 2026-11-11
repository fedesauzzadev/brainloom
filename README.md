# brainloom

Criterion, limits, and memory for AI-assisted development.

A versioned, tool-agnostic methodology kit: a persistent project **brain** (a
markdown graph with pointers into the code), impact-radius **triage**, vertical
**slices**, and **real verification**. Install once, use in any project, update
without losing data.

> Full bilingual (EN/ES) documentation ships with v0.1.0. Kit content is in English.

## Development

- Every skill carries a `## Verification` contract (fixture + task + expected
  artifacts). Run `node scripts/smoke.mjs` before versioning; `--agent` runs
  the contracts through the harness. A skill change without its smoke check
  stays unverified.
- Kit scripts are plain Node `.mjs`, stdlib only, cross-platform. Anything
  else must be ASCII-only or UTF-8 with BOM (Windows PowerShell 5.1 reads
  BOM-less UTF-8 as ANSI) — `smoke.mjs` enforces it.
