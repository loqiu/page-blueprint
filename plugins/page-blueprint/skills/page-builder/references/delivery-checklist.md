# Delivery Checklist

Run this checklist before you finish implementation work.

## Structural Fidelity

- Does the implemented route match the blueprint route intent?
- Are the top-level modules present and ordered correctly?
- Is the dominant surface still dominant?
- Are supporting rails, drawers, or detail panels placed correctly?

## Behavioral Fidelity

- Do the implemented actions match the blueprint?
- Are filtering, sorting, drill-down, and return patterns preserved?
- Are blocked or dangerous actions handled as specified?

## State Fidelity

- Are required loading, empty, error, disabled, stale, and restricted states implemented?
- Are those states local to the correct modules rather than only global banners?

## Visual Fidelity

- Does the page density match the visual reference?
- Are spacing and hierarchy aligned with the mock and shared design rules?
- Has the implementation avoided decorative drift or generic dashboard styling?
- Is there still exactly one dominant surface?
- Did the page avoid giant hero chrome, equal-weight floating cards, and other anti-patterns forbidden by the shared guide unless explicitly requested?

## Code Quality

- Were existing components reused where possible?
- Is every new component justified by a blueprint module?
- Are route placement and component ownership clear?
- Did you avoid one-off hacks that fight the codebase?
