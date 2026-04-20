# Page Blueprint Public Skills

This branch is the self-contained public distribution layer for:

- `page-blueprint`
- `page-builder`

It is intentionally different from the main development branch:

- each skill is self-contained
- shared design and guide dependencies are bundled inside each skill
- the branch is shaped for `npx skills add ...` style installation

## Install

List available skills:

```bash
npx skills add https://github.com/loqiu/page-blueprint/tree/public-skills --list
```

Install both skills for Codex:

```bash
npx skills add https://github.com/loqiu/page-blueprint/tree/public-skills --skill page-blueprint page-builder -g -a codex -y --copy
```

Install only one skill:

```bash
npx skills add https://github.com/loqiu/page-blueprint/tree/public-skills --skill page-blueprint -g -a codex -y --copy
```

After install, restart Codex.
