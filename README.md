# [中文](README.zh-CN.md) | English

# Page Blueprint

> Blueprint-first frontend page planning and implementation skills for Codex.

![Codex](https://img.shields.io/badge/Codex-Skills-111827?style=flat-square)
![Workflow](https://img.shields.io/badge/Workflow-Blueprint%20%E2%86%92%20Builder-2563eb?style=flat-square)
![Shell](https://img.shields.io/badge/Shell%20Mode-Workspace%20%7C%20Centered-0f766e?style=flat-square)
![Figma](https://img.shields.io/badge/Figma-MCP%20Ready-f97316?style=flat-square)
![License](https://img.shields.io/badge/License-GPL--2.0-16a34a?style=flat-square)
![Release](https://img.shields.io/badge/Release-v0.1.1-7c3aed?style=flat-square)

Page Blueprint is a dual-skill repository for Codex:

- `page-blueprint`: turns product goals, design rules, screenshots, and repo context into a reviewable page blueprint document.
- `page-builder`: turns an approved blueprint into UI code without drifting from route, hierarchy, states, copy, or shell mode.

This repo is built for real product pages, not isolated mockups. It pushes Codex to decide page mode first, keep one dominant surface, respect route/context/state realism, and avoid decorative demo-dashboard patterns.

## Quick start

### Install as skills

```powershell
python "$env:USERPROFILE\.codex\skills\.system\skill-installer\scripts\install-skill-from-github.py" `
  --repo loqiu/page-blueprint `
  --path skills/page-blueprint skills/page-builder `
  --ref v0.1.1
```

Then restart Codex.

Current recommended version: `v0.1.1`

### First-run prompt

```text
Use page-blueprint with this frontend repo.
Inspect the project, recommend the best first target page, decide page mode and shell mode,
and draft an approved blueprint before any code changes.
```

## What ships in `v0.1.1`

- Dual skill workflow:
  - `skills/page-blueprint`
  - `skills/page-builder`
- Shared design intelligence:
  - global design rules
  - page-mode design sources
  - professional page generation rules
  - shell mode rules: `workspace shell` vs `centered page`
- Builder handoff structure:
  - implementation appendix
  - pre-code summary
  - verification contract
- Example artifact:
  - `shared/examples/moneykeeper-vue-statistics-blueprint.md`
- Figma-friendly planning flow for turning blueprints into editable design structure
- First plugin packaging layer:
  - `plugins/page-blueprint/`
  - `.agents/plugins/marketplace.json`

## Why this repo exists

Typical AI-generated admin pages fail in the same ways:

- they look like centered design canvases instead of application shells
- they treat KPI, chart, table, and rail as equal-weight modules
- they overuse hero blocks, gradients, floating cards, and generic dashboard patterns
- they write code before clarifying page mode, dominant surface, route context, and real product states

This repository fixes that by making Codex follow a stricter sequence:

1. understand the page
2. classify the page
3. decide shell mode
4. write the blueprint
5. optionally generate Figma / mock structure
6. build code from the approved blueprint

## Repository layout

```text
skills/
  page-blueprint/
  page-builder/
shared/
  design/
    global/
    page-modes/
  examples/
  guides/
output/
  imagegen/
plugins/
  page-blueprint/
.agents/
  plugins/
docs/
```

## Core concepts

### 1. Blueprint is mandatory

`page-builder` should not start from screenshots alone.  
The approved blueprint is the logic source of truth.

### 2. Shell mode is structural, not decorative

- `workspace shell`
  - persistent system node
  - left rail / utility chrome / fluid content width
  - medium-high to high density
  - suitable for consoles, workbenches, dashboards
- `centered page`
  - bounded content canvas
  - page-level task focus
  - low to medium density
  - suitable for auth, onboarding, payment, detail forms

### 3. Visual redesign is not a skin change

When the blueprint says `visual-redesign`, the result must visibly change:

- shell strategy
- first-screen order
- dominant surface
- module hierarchy

Spacing-only rewrites do not count.

## Install in Codex

This repository now ships in two installable forms:

- versioned **skills** from the repo root
- a repo-local **plugin package** under `plugins/page-blueprint/`

### Recommended install path

For most users, the most stable path is still installing the skills by tag with Codex's built-in skill installer:

- repo: `loqiu/page-blueprint`
- ref: `v0.1.1`
- paths:
  - `skills/page-blueprint`
  - `skills/page-builder`

### Script install

Windows:

```powershell
python "$env:USERPROFILE\.codex\skills\.system\skill-installer\scripts\install-skill-from-github.py" `
  --repo loqiu/page-blueprint `
  --path skills/page-blueprint skills/page-builder `
  --ref v0.1.1
```

macOS / Linux:

```bash
python ~/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py \
  --repo loqiu/page-blueprint \
  --path skills/page-blueprint skills/page-builder \
  --ref v0.1.1
```

After install:

1. Restart Codex.
2. Use `page-blueprint` to draft a page blueprint.
3. Use `page-builder` to implement from the approved blueprint.

Detailed install instructions:

- [Plugin and skills install guide](docs/INSTALL.md)

## Upgrade

### Skills

Re-run the install command against the new tag:

```powershell
python "$env:USERPROFILE\.codex\skills\.system\skill-installer\scripts\install-skill-from-github.py" `
  --repo loqiu/page-blueprint `
  --path skills/page-blueprint skills/page-builder `
  --ref v0.1.1
```

Then restart Codex.

### Plugin

1. Download the latest plugin zip from the newest release.
2. Replace your local `page-blueprint` plugin directory.
3. Restart Codex.

## Plugin package

This repo now also contains a plugin package:

- `plugins/page-blueprint/.codex-plugin/plugin.json`

That package includes self-contained copies of:

- `skills/`
- `shared/`
- plugin metadata
- plugin assets

### Important install note

Codex currently has a built-in **skill installer** workflow, but not the same remote one-command installer for GitHub-hosted plugins.

So today:

- the easiest remote install path is still the **skills** install shown above
- the bundled plugin package is best used by cloning or unpacking the repo locally and exposing `plugins/page-blueprint/` through a local marketplace entry

This means the release is now **plugin-packaged**, but Codex does not yet treat a GitHub release asset as a one-click plugin install source by default.

## Local plugin install

If you want to use the packaged plugin instead of installing the two skills directly:

1. Clone this repository locally or download the plugin zip from the latest release.
2. Place `plugins/page-blueprint/` under your local plugin root, for example:
   - Windows: `%USERPROFILE%\plugins\page-blueprint`
   - macOS / Linux: `~/plugins/page-blueprint`
3. Create or update your local marketplace file:
   - Windows: `%USERPROFILE%\.agents\plugins\marketplace.json`
   - macOS / Linux: `~/.agents/plugins/marketplace.json`
4. Add this entry:

```json
{
  "name": "page-blueprint",
  "source": {
    "source": "local",
    "path": "./plugins/page-blueprint"
  },
  "policy": {
    "installation": "AVAILABLE",
    "authentication": "ON_INSTALL"
  },
  "category": "Coding"
}
```

5. Restart Codex.

The repository already includes a repo-local example marketplace file at `.agents/plugins/marketplace.json`.

## Suggested first-run workflow

### If you already have a UI repo

1. Give Codex the repo path.
2. Let `page-blueprint` inspect the project.
3. Confirm:
   - target page
   - page mode
   - shell mode
   - `safe-refactor` or `visual-redesign`
4. Approve the blueprint.
5. Optionally push the blueprint into Figma.
6. Run `page-builder`.

Example:

```text
Use page-blueprint with C:\WorkSpace\Vue\moneykeeper-vue.
Inspect the repo first, recommend the best first target page,
and draft an approved blueprint in visual-redesign mode.
```

### If you do not have a UI repo yet

1. Start with `page-blueprint` in greenfield mode.
2. Define:
   - target page
   - primary user
   - primary task
   - page mode
   - shell mode
3. Produce the blueprint first.
4. Optionally create Figma structure from that blueprint.
5. Build code only when a real target codebase exists.

## FAQ

### Is this repo better installed as skills or as a plugin?

Today, install as skills if you want the shortest remote setup path.  
Use the plugin package if you want a local plugin-style bundle with plugin metadata and marketplace wiring.

### Can I install directly from a GitHub release asset?

For the skills workflow, the stable path is still installing by repo + tag through Codex's skill installer.  
For the plugin workflow, the release zip is mainly a convenient local unpack target.

### Do I need a UI repo to use this?

No. Without a UI repo, start in greenfield mode with `page-blueprint`. The output becomes a product-grade page blueprint, not a repo-specific implementation plan.

### Do I need Figma?

No. Figma is optional. It becomes useful when you care about exact module positions, proportions, and visual composition beyond what the blueprint can specify in text.

## Versioning

This repository is intended to evolve through tagged releases.

- `v0.1.0`: first public dual-skill release
- `v0.1.1`: plugin packaging added on top of the dual-skill release

See [CHANGELOG.md](CHANGELOG.md) for release-level changes.

## License

This repository is released under the GNU GPL-2.0 license. See [LICENSE](LICENSE).
