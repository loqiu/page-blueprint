# Professional Page Generation Guide

Use this guide to keep generated pages product-grade instead of template-grade.

This guide complements the shared design docs. It does not replace:

- `../design/global/Global-Design.md`
- `../design/global/DESIGN-AGENTS.md`
- the page-mode documents under `../design/page-modes/`

## Core Priority Order

Always prioritize in this order:

1. user task clarity
2. information hierarchy
3. dominant working surface
4. operational realism
5. system consistency
6. visual polish

Do not improve polish by sacrificing:

- scan speed
- route or context clarity
- table readability
- state clarity
- action placement
- component consistency

## Mandatory Pre-Code Decisions

Before implementation, the page plan or pre-code summary must explicitly state:

1. page mode
2. primary user task
3. first 10-second information need
4. dominant surface
5. shell mode
6. route position and page context
7. layout hierarchy
8. key modules
9. action placement
10. state handling
11. reuse plan

## Supported Page Modes

### Overview Dashboard
- purpose: KPI summary, trend review, business or strategy overview
- dominant surface: KPI + one dominant trend or comparison region
- avoid: putting table/list above the summary region, giant decorative hero, equal-weight widgets

### Monitoring Dashboard
- purpose: runtime state, health visibility, alert handling, freshness awareness
- dominant surface: status strip, alert region, health region
- avoid: decorative charts outranking incidents, hiding stale data in footnotes

### Operations Dashboard
- purpose: queue handling, proposal/execution lists, action-heavy work
- dominant surface: table/list
- avoid: replacing row comparison with loose cards, burying the list below decorative analytics

### Detail Page
- purpose: one object, one execution, one investigation, one task
- dominant surface: summary header + primary detail sections
- avoid: giant banner openings, decorative hero space, shallow tabs hiding weak hierarchy

### Browse / Discovery Page
- purpose: browse, compare lightly, discover objects, narrow with filters
- dominant surface: result list, result grid, or object-first browse surface
- avoid: forcing dashboard language onto a browse task, overloading the top area with KPI chrome

### Settings / Admin Page
- purpose: configure rules, manage permissions, edit preferences, review operational configuration
- dominant surface: structured form sections, admin tables, or policy groups
- avoid: turning settings into a dashboard, hiding consequences of actions, decorative layouts that obscure scope

## Dominant Surface Rule

Each page may have many modules, but only one dominant surface.

Do not let KPI, chart, table, rail, and detail panel all compete as co-equals.

## Shell Mode Rule

Choose one shell mode explicitly:

- `workspace shell`
- `centered page`

Use `workspace shell` for tool-like pages that live inside a persistent application frame.
Use `centered page` for page-level tasks, focused forms, auth, onboarding, or bounded reading flows.

Do not mix the two by placing a narrow centered canvas inside a fake dashboard shell.
Do not default to `centered page` for dashboards, analytics workbenches, or admin surfaces.

## Hierarchy Rule

Always separate:

- primary information
- secondary information
- supporting information
- low-priority information

Required behavior:

- keep the first screen focused on the most important judgment or action
- demote supporting context below or beside the main task
- do not let history, metadata, or help copy outrank the main object or main work surface

## Density Rule

Recommended density by page mode:

- overview dashboard: medium
- monitoring dashboard: medium-high
- operations dashboard: high
- detail page: medium
- browse/discovery page: low-medium
- settings/admin page: medium

Do not make tool pages look like marketing pages.

## Visual Restraint Rule

Allowed:

- clean neutrals
- semantic state colors
- limited accent usage
- subtle border structure
- moderate spacing
- compact and readable modules

Forbidden by default:

- decorative gradients
- glassmorphism
- glowing borders
- oversized shadows
- giant rounded pills everywhere
- colorful sections without semantic meaning
- brand color used decoratively across the whole page

## Table vs Card Rule

Use table/list when the task is:

- compare across rows
- scan many items
- sort
- inspect multiple fields
- act in queue-like work

Use cards when:

- object-first browsing matters more than row comparison
- low-density summary matters more than scanning efficiency

Do not switch from table to cards only to look more modern.

## Action Rule

Always distinguish:

- primary action
- secondary action
- contextual action
- destructive action
- overflow action

Required behavior:

- primary action is obvious
- destructive action is visually separated
- disabled actions explain why they are unavailable
- row actions never overpower row identity

## Route and Context Rule

Every page is a node in a real system, not a standalone screenshot.

Always define:

- route
- parent route
- entry points
- drill-down destinations
- return context
- whether filters or selection context should be preserved

## List-Detail Relationship Rule

List pages should support:

- scan
- filter
- sort
- quick compare
- lightweight action
- lightweight inspection

Detail pages should support:

- identity
- status
- evidence
- context
- history
- deeper action

Use split view, drawer, or expandable row for lightweight inspection before forcing a full page transition.

## Real Product States Rule

Important pages and important modules must consider:

- loading
- empty
- error
- disabled
- stale / outdated
- no results after filters
- permission-restricted
- partial failure

Required behavior:

- prefer skeletons over spinner-only loading
- explain why empty exists
- make stale visible
- isolate section-level failure when possible
- keep unaffected modules visible during partial failure

## Copy Rule

Use tool-like copy:

- short
- precise
- action-oriented
- non-marketing

Avoid vague verbs such as:

- Explore
- Discover
- Magic
- Boost
- Supercharge

## Reuse and Engineering Rule

Prefer reuse before invention:

- PageHeader
- FilterBar
- SummaryStrip
- StatusBadge
- MetricCard
- DataTable
- EmptyState
- ErrorState
- SectionError
- MetadataGrid
- DetailSection
- Timeline
- SideDrawer
- InlineNotice
- FreshnessTag

Use shared tokens, shared layout primitives, stable component patterns, and consistent state handling.

Avoid:

- page-specific visual hacks
- random spacing values
- one-off colors
- repeated bespoke UI for the same pattern

## Anti-Patterns

Do not generate these unless the user explicitly asks for them:

- giant hero banner on business pages
- marketing-style landing layout for dashboards
- decorative gradient backgrounds
- full-page glass cards
- oversized KPI cards with low information density
- every section as a floating card
- multi-color badges everywhere
- charts with no decision value
- equal-weight dashboard widgets by default
- card waterfall replacing an operational table
- action overload in the header
- tabs hiding weak hierarchy
