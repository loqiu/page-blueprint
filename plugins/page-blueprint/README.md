# Page Blueprint Plugin

This plugin packages the Page Blueprint workflow as a repo-local Codex plugin.

It currently bundles:

- `page-blueprint`
- `page-builder`

plus the shared design intelligence layer they depend on:

- global design rules
- page-mode design sources
- professional page generation rules
- shell mode rules
- example blueprint artifacts

## What this plugin is for

Use this plugin when you want Codex to:

- inspect a frontend repo before changing UI
- classify a target page by page mode
- decide `workspace shell` vs `centered page`
- write an implementation-ready page blueprint
- build from the approved blueprint without drifting into generic AI dashboard UI

## Plugin structure

- `.codex-plugin/plugin.json`
  - plugin manifest and UI metadata
- `agents/openai.yaml`
  - plugin-level prompt metadata
- `skills/`
  - packaged copies of the two core skills
- `shared/`
  - packaged design and guide references used by those skills
- `assets/`
  - plugin icon assets

## Notes

This plugin is self-contained inside `plugins/page-blueprint/`.
It is intended for local plugin installation or future plugin-oriented release packaging.
