# Changelog

All notable changes to this project are documented here.
Format: [Keep a Changelog](https://keepachangelog.com/en/1.1.0/); versioning: [SemVer](https://semver.org/).
Entries that change the brain format, config, or skill contracts are marked **[BREAKING]**.

## [Unreleased]

## [0.1.0] - 2026-11-09

### Added
- Core brain templates (`schema_version: 1`): index, vision, roadmap, conventions, shared registry, node, decision, config.
- Skills: `triage` (impact-radius classification and routing), `memory-update` (closing the loop: nothing is done until the brain reflects it).
- `AGENTS.md` instance template.
- Repo skeleton: `/core` (tool-agnostic), `/adapters/opencode`, `/scripts`, `/tests`.
