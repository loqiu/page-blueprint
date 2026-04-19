# Source Priority

Use this order whenever sources disagree.

## 1. Blueprint: logic source of truth

The approved blueprint controls:

- redesign level
- shell decision
- route intent
- information architecture
- module list and ordering
- component responsibilities
- required states
- business copy
- primary and secondary actions

## 2. Shared design docs: design rule source of truth

The shared design docs under `../../../shared/design/` plus `../../../shared/guides/professional-page-generation.md` control:

- global tokens and semantics
- page-mode behavior
- density expectations
- accessibility minimums
- state treatment expectations
- dominant surface discipline
- table-vs-card decisions
- route/context realism
- anti-pattern avoidance

## 3. Visual reference: layout and polish source of truth

The mock, screenshot, or high-fidelity image controls:

- layout proportions
- spacing rhythm
- hierarchy emphasis
- alignment
- visual density
- surface treatment

Do not let it create new features or workflow rules.

## 4. Codebase: implementation source of truth

The target codebase controls:

- actual file placement
- framework-specific patterns
- reusable component inventory
- state/data wiring patterns
- token and styling APIs

## Conflict Rules

- Blueprint vs mock: blueprint wins on behavior, mock wins on presentation.
- Blueprint vs codebase: stop and surface the mismatch if user-facing behavior would change.
- Blueprint vs existing page shell: if the blueprint explicitly says `bypass`, the shell does not get to win by inertia.
- Mock vs codebase: prefer codebase primitives if the visual outcome remains faithful enough.
- Shared design docs vs mock: design docs win when the mock violates tokens, accessibility, or page-mode rules.
