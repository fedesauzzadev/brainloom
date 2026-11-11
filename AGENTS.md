# AGENTS.md — brainloom kit (this repo)

> This repo SHIPS the brainloom kit. It is held to the kit's own standard:
> small verified steps, real memory, no monsters.

## Non-negotiable: TODO se verifica

Every claim of "done / works / verified / passes" must be backed by a command
that was actually executed and its observed result, shown in the reply.
"Should work", "probably passes", "CI will run it" = NOT verified = NOT done.
If something cannot be verified (no infra, no credentials), say so explicitly
and mark the work accordingly — never present it as done.

## Kit development rules

1. Before versioning: `node scripts/smoke.mjs` (structural) must pass, and any
   skill/flow the change touches gets its `--agent` contract run (real harness)
   or stays unverified.
2. CI steps are bash-pinned; verify each `run:` command locally under bash
   (`git bash` works) exactly as written before pushing a workflow change.
   Remotes: `origin` (local bare) and `github` (fedesauzzadev/brainloom,
   public — GitHub Actions runs the CI there for real).
3. Follow Keep-a-Changelog + SemVer; additive brain-format fields need no
   schema bump (precedent: `verify:` 0.3.0, `verification.level` 0.4.0);
   breaking changes ship a migration in the same change.
4. Repo layout: `/core` (tool-agnostic content), `/adapters/opencode`,
   `/scripts` (portable Node stdlib-only .mjs), `/tests` (fixtures + fake
   agent). Any `.ps1`/`.cmd`/`.bat` must be ASCII-only or UTF-8 BOM.
5. This repo has no brain/ yet — full init-brain dogfooding is a pending
   decision. Until then, THIS file is the repo's memory: update it when a
   rule changes, and record durable decisions in CHANGELOG.md entries.
