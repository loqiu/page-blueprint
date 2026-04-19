# Changelog

All notable changes to this repository will be documented in this file.

## v0.1.1 - 2026-04-19

### Added

- first repo-local plugin package at `plugins/page-blueprint/`
- plugin manifest at `plugins/page-blueprint/.codex-plugin/plugin.json`
- plugin-level assets and agent metadata
- self-contained plugin copies of `skills/` and `shared/`
- repo-local marketplace entry at `.agents/plugins/marketplace.json`
- root-level `PRIVACY.md` and `TERMS.md`

### Notes

- `v0.1.1` keeps the repo installable as skills and also packages it as a local plugin.
- Codex still has the most direct remote install path for the skills form, via `skill-installer`.

## v0.1.0 - 2026-04-19

### Added

- Public dual-skill repository structure:
  - `skills/page-blueprint`
  - `skills/page-builder`
- Shared design intelligence layer under `shared/`:
  - global design rules
  - page-mode design sources
  - shell mode reference
  - professional page generation rules
- `page-blueprint` support for:
  - page mode classification
  - `workspace shell` vs `centered page`
  - `safe-refactor` vs `visual-redesign`
  - implementation appendix for builder handoff
- `page-builder` support for:
  - pre-code summary
  - source-priority locking
  - codebase intake rules
  - verification contract
- Example blueprint:
  - `shared/examples/moneykeeper-vue-statistics-blueprint.md`
- Generated sample visual assets under `output/imagegen/`

### Notes

- `v0.1.0` is a versioned skills release, not a Codex plugin package.
- Codex should install the skills from this repo by tag/ref, not from a release asset.
