# Build Input Contract

Use this reference before implementing a page from a blueprint.

## Required Inputs

Do not begin full implementation until you have:

- an approved blueprint document
- the target codebase or target workspace

## Optional but Valuable Inputs

Use these when available:

- a high-fidelity visual reference
- screenshots of the current page
- an approved generated mock
- acceptance criteria or QA notes

## Strongly Recommended Inputs

Capture these when available:

- target route
- framework and routing stack
- existing page or component to replace
- design system or component library constraints
- entry points and drill-down destinations
- whether selection or filter context must be preserved

## Blocking Conditions

Stop and ask before coding when:

- there is no approved blueprint
- the target framework is unknown
- the user wants code but no codebase is available
- the same page has two conflicting blueprint versions
- the route target is unclear and would change file placement

## Minimal Safe Fallback

If the user insists on implementation with partial inputs:

1. require the blueprint
2. infer visual fidelity from the provided mock or screenshot only if one exists
3. mark unknown route or data wiring details as blocked questions

Do not improvise core business behavior.
