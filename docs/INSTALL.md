# Install Guide

This repository can be used in two forms:

1. **Skills install**
2. **Local plugin install**

For most users, **skills install is the fastest path**.

Current documented version: `v0.1.1`

Important branch split:

- `main`: source-of-truth development branch
- `public-skills`: self-contained public install branch for `npx skills add ...`

## 1. Install as skills

Use Codex's built-in skill installer against a tagged release.

### Windows

```powershell
python "$env:USERPROFILE\.codex\skills\.system\skill-installer\scripts\install-skill-from-github.py" `
  --repo loqiu/page-blueprint `
  --path skills/page-blueprint skills/page-builder `
  --ref v0.1.1
```

### macOS / Linux

```bash
python ~/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py \
  --repo loqiu/page-blueprint \
  --path skills/page-blueprint skills/page-builder \
  --ref v0.1.1
```

### After install

1. Restart Codex.
2. Start with `page-blueprint`.
3. Only after the blueprint is approved, use `page-builder`.

### Upgrade

To upgrade skills, re-run the same install command with the newer tag:

```powershell
python "$env:USERPROFILE\.codex\skills\.system\skill-installer\scripts\install-skill-from-github.py" `
  --repo loqiu/page-blueprint `
  --path skills/page-blueprint skills/page-builder `
  --ref v0.1.1
```

Then restart Codex.

### Public `npx skills` install

If you are installing through the `skills.sh` / `npx skills` workflow, use the public distribution branch instead of `main`:

```bash
npx skills add https://github.com/loqiu/page-blueprint/tree/public-skills --skill page-blueprint page-builder -g -a codex -y --copy
```

## 2. Install as a local plugin

Use this path when you want the bundled plugin package with:

- `.codex-plugin/plugin.json`
- plugin metadata
- plugin-local `skills/`
- plugin-local `shared/`
- plugin-local assets

### Step 1: place the plugin directory locally

You need a local plugin root:

- Windows: `%USERPROFILE%\plugins`
- macOS / Linux: `~/plugins`

The final plugin path should be:

- Windows: `%USERPROFILE%\plugins\page-blueprint`
- macOS / Linux: `~/plugins/page-blueprint`

You can populate that path in either of these ways:

- clone this repository and copy `plugins/page-blueprint/`
- download the `page-blueprint-plugin-v0.1.1.zip` asset from the release and extract it there

### Step 2: create or update marketplace.json

Create this file if it does not exist:

- Windows: `%USERPROFILE%\.agents\plugins\marketplace.json`
- macOS / Linux: `~/.agents/plugins/marketplace.json`

Minimal file shape:

```json
{
  "name": "local-marketplace",
  "interface": {
    "displayName": "Local Plugins"
  },
  "plugins": [
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
  ]
}
```

If your marketplace file already exists, append only the plugin entry inside `plugins[]`.

### Step 3: restart Codex

After restart, Codex can discover the plugin through your local marketplace.

### Upgrade

To upgrade the local plugin:

1. Download the latest plugin zip from the newest GitHub release.
2. Replace your local `page-blueprint` plugin directory.
3. Restart Codex.

## Which install form should I choose?

### Choose skills install if:

- you want the shortest remote install path
- you want to install by GitHub repo + tag
- you do not need plugin marketplace metadata

### Choose local plugin install if:

- you want a bundled plugin directory
- you want plugin metadata and local marketplace wiring
- you are distributing this repository internally as a local Codex plugin
