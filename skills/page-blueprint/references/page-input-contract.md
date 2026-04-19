# Page Input Contract

Use this reference when the user gives a vague page target or only partial source materials.

## Minimum Inputs

Capture these fields before drafting a full blueprint:

- `page_name`: the page being planned or rewritten
- `core_entity`: the main business object, if one exists
- `primary_user`: who uses the page
- `primary_task`: what the user wants to finish in the first 10 seconds
- `source_materials`: PRD, screenshots, route list, API fields, table columns, notes, or existing docs

If one of the first four fields is missing and the missing information would change the page structure, ask before drafting.

If there is no repo, also capture:

- whether this is a greenfield page or a redesign of an existing design
- preferred shell mode: `workspace shell` or `centered page`

## Helpful Inputs

When available, also capture:

- project path or repo root
- current route or candidate route
- preferred shell mode: `workspace shell` or `centered page`
- upstream and downstream pages
- main states and lifecycle labels
- permissions or role differences
- key actions and destructive actions
- table columns, metrics, filters, or section inventory
- domain glossary and naming conventions

## First-Use Repo Intake

If the user provides a project path but does not yet specify a page:

1. inspect the repo structure first
2. identify candidate pages that match the supported page modes
3. recommend a first target page before drafting any blueprint

Do not force a blueprint for an arbitrary page when the repo can tell you which page is the better starting point.

If there is no repo:

1. do not fabricate route files, component paths, or implementation ownership
2. draft a greenfield blueprint first
3. treat implementation details as deferred until a real codebase exists

## Evidence Order

Prefer evidence in this order:

1. explicit user requirements
2. project documentation and screenshots
3. existing route, component, and copy conventions
4. careful inference from the page mode

Do not let step 4 override steps 1 to 3.

## Safe Inference Boundary

You may infer:

- the dominant page mode
- the likely dominant surface
- the rough module ordering
- standard state coverage
- common UX copy patterns such as empty-state guidance

Do not infer without labeling the assumption when it affects:

- route families
- workflow states
- permission boundaries
- irreversible actions
- SLA, freshness, or severity semantics
- business nouns used in the UI

## Clarification Triggers

Pause and ask a concise question when any of these are unclear:

- the page serves two competing primary tasks
- the main business object is unknown
- the primary action is ambiguous
- shell choice would materially affect navigation placement, content width, or information density
- route placement could belong to different route families
- the same label could mean different domain concepts
