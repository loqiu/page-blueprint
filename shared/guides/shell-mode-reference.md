# Shell Mode Reference

Use this guide to decide whether a page should be implemented as a `workspace shell` or a `centered page`.

This is a structural decision, not a visual adjective.

## Workspace Shell

Choose `workspace shell` when the page behaves like a persistent node inside a larger application.

Typical signals:

- the page is used frequently
- users move between sibling tools without leaving the product shell
- left navigation, top utility chrome, or persistent context matters
- information density should stay medium-high or high
- the main content should use fluid width instead of sitting inside a centered canvas
- the page feels like a console, control panel, workbench, dashboard, or admin tool

Typical examples:

- overview dashboards in a product console
- monitoring dashboards
- operations pages
- multi-section analytics pages
- admin pages with persistent side navigation

Expected layout traits:

- app-level navigation rail or utility bar
- content area expands with the shell grid
- content scroll happens inside the main app region
- modules feel attached to the application frame, not placed on a showcase canvas

Do not choose `workspace shell` only because a page has a chart or a sidebar.

## Centered Page

Choose `centered page` when the page is primarily a page-level task surface rather than an application shell surface.

Typical signals:

- the page serves one focused task or one self-contained flow
- readability, form completion, or narrative explanation matters more than persistent chrome
- medium or low density is acceptable
- the page benefits from a bounded canvas width
- the page feels like a form, auth page, onboarding page, payment page, or single-object detail page

Typical examples:

- login or registration
- onboarding and first-run
- payment / success / cancel pages
- focused settings forms
- some detail pages with one primary object and limited surrounding context

Expected layout traits:

- bounded content width
- page-level composition inside a centered canvas
- content scroll happens at the page level
- visual emphasis stays on the task surface, not on persistent app chrome

Do not choose `centered page` only because the page should look refined.

## Decision Questions

Answer these before locking shell mode:

1. Is the user operating inside a persistent application workspace?
2. Does navigation chrome need to remain visible while the user works?
3. Would a centered canvas reduce useful density or make the page feel like a demo?
4. Is the page primarily one self-contained task instead of one node in a larger tool?

If questions 1 to 3 are mostly yes, prefer `workspace shell`.
If question 4 is yes and the first three are mostly no, prefer `centered page`.

## Red Flags

`workspace shell` is probably wrong when:

- the page becomes mostly empty chrome around a small form
- the page uses a full app frame but only needs one narrow task surface

`centered page` is probably wrong when:

- the page holds dashboards, workbench tools, or dense analysis content
- the page looks like a poster floating in the middle of an app
- the user needs persistent context while comparing multiple modules
