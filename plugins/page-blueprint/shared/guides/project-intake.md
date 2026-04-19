# Project Intake

Use this guide the first time a user points the skills at a frontend repository, especially when they provide a project path before naming a target page.

If there is no UI repo yet, do not run repo intake. Start with a greenfield blueprint instead.

## Goal

Inspect the repository first, then decide:

- which page is the best starting point
- which page mode it likely maps to
- whether the work should begin with `$page-blueprint`
- what codebase constraints will shape later implementation

Do not choose a starting page from the screenshot alone when the repo structure can answer the question better.

## First-Use Trigger

Run project intake when any of these are true:

- the user gives a project path but no target page
- this is the first time working in the repo
- the target page is named vaguely and could refer to multiple routes
- the user asks where to start

Skip project intake when:

- the user has no UI repo yet
- the user wants to generate a greenfield page from scratch
- there is no existing route or codebase to inspect

## Repo Questions To Answer

Inspect the project and answer these questions:

- Which framework, router, UI library, and state library are in use?
- Where do routes and page entry files live?
- Which pages already exist?
- Which pages best match the currently supported page modes?
- Where are shared layout shells, page shells, and reusable components?
- How are auth, API modules, composables, stores, and i18n organized?
- Which commands run lint, build, and any other verification?

## First-Page Selection Rule

Prefer a first target page that:

- clearly matches an existing supported page mode
- has enough complexity to validate the method
- is already a real page in the repo
- does not depend on unknown hidden flows

Avoid choosing a first page that is:

- too trivial to validate blueprint quality
- outside the current design-source coverage
- mostly auth plumbing or legal copy
- blocked by missing app context

## Recommended Output

After intake, give a short recommendation:

1. what the repo stack is
2. which pages are the best candidates
3. which page should be first
4. why
5. whether to start with `$page-blueprint`

## No-Repo First Use

If the user has no UI repo:

1. do not pretend there is implementation context
2. start with `$page-blueprint` in greenfield mode
3. collect:
   - target page
   - primary user
   - primary task
   - page mode
   - shell mode
   - safe-refactor vs visual-redesign does not apply unless there is an existing design to replace
4. produce a blueprint first
5. optionally generate a Figma structure or mock
6. only start `$page-builder` after a real codebase exists or the user explicitly asks for a fresh implementation target

## Example Decision Pattern

- Login or register pages are often good warm-up tasks, but weak first validation targets if the skill's design sources mainly cover dashboards and detail pages.
- A statistics page is often a better first target when overview dashboard rules already exist.
- A notifications or monitoring-style page is often a strong second target.
