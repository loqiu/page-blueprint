# Changelog

All notable changes to this repository will be documented in this file.

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
