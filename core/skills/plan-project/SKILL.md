---
name: Brainloom Plan Project
description: Decompose a whole project idea into ordered vertical slices with dependencies, shared-code candidates, and risks; record them in brain/roadmap.md after explicit user approval. Use when starting a new project (or re-planning one), before building the first slice, or when the user asks for a plan or roadmap.
---

# Plan Project

Input: the WHOLE idea. Output: an approved roadmap of vertical slices.
The plan is a proposal — nothing is recorded until the user approves.

## 1. Understand the idea
- Restate it in 2-5 sentences: what it is, who uses it, what "done" looks like.
- Read `brain/vision.md`; if the idea contradicts it, surface the conflict.

## 2. Ask (blocking, grouped, numbered, with recommendations)
Purpose/scope unknowns, hard constraints, and tech choices ONLY if they gate the
design. Assume the rest; record assumptions as reversible decisions in
`brain/decisions/` and list them in the final proposal.

## 3. Propose slices
A vertical slice is the minimum that crosses ALL layers and works end-to-end.
- **Slice 1 = walking skeleton**: the thinnest possible end-to-end path (one
  input → one output, touching every layer once). It validates the architecture
  and leaves extension points. If it cannot be thin, the architecture is wrong —
  say so and propose a different shape.
- Following slices: one coherent capability each, growing the skeleton. Reuse
  the patterns the skeleton established; never introduce a parallel architecture.
- Order by dependency; flag slices that could run in parallel.

## 4. For each slice, state
- Goal as observable behavior ("after this, the user can ...").
- Nodes it will likely produce (M-sized; trivial S tasks get folded in).
- What it reuses vs what it introduces.
- Its main risk, and what would force a split or reorder.

## 5. Shared code
- Intra-project candidates (used by 2+ slices) → note as CANDIDATES for
  `brain/shared/registry.md` (rule of three still applies — do not pre-abstract).
- Cross-project reusable patterns → registry candidates tagged `cross-project`.

## 6. Risks
Top risks, one mitigation each (spike slice, fallback, cut).

## 7. Approval → record
- Present the proposal; WAIT for the user's OK (adjust and re-present if not).
- On approval: write the slices into `brain/roadmap.md` (backlog table, slice 1
  as current), the risks, and update `brain/index.md`.

## Existing codebase?
This skill plans new or re-planned projects. To map an existing codebase into
the brain, use `adopt` instead.
