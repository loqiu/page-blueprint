---
name: page-builder
description: Build frontend page implementations from an approved page blueprint, shared design rules, and a visual reference. Use when Codex needs to turn a finalized page blueprint into real UI code without drifting from the intended route, information architecture, component contracts, states, or business copy.
---

Implement approved page blueprints in code. Treat the blueprint as the logic source of truth, the mock or screenshot as the visual source of truth, and the target codebase as the implementation source of truth.

## Canonical Flow

Always follow this sequence:

1. shared design sources
2. approved page blueprint
3. optional high-fidelity mock or screenshot
4. implementation in the target codebase

The visual reference is optional. The blueprint is not optional.

## Workflow

1. Confirm the source package.
   - If this is the first contact with the repo, read `../../shared/guides/project-intake.md` before deciding how to apply the builder.
   - Read [references/build-input-contract.md](references/build-input-contract.md).
   - Read `../../shared/guides/professional-page-generation.md`.
   - Read `../../shared/guides/shell-mode-reference.md`.
   - If there is no approved blueprint document, stop and ask to run `$page-blueprint` first.
2. Gather sources in this order.
   - Approved blueprint document.
   - Shared design docs under `../../shared/design/`.
   - Visual reference: high-fidelity mock, screenshot, or generated blueprint image.
   - Existing codebase routes, layout primitives, components, tokens, and state patterns.
   - Read [references/codebase-intake.md](references/codebase-intake.md) before deciding file placement or component ownership.
3. Lock source priority.
   - Read [references/source-priority.md](references/source-priority.md).
   - If the mock conflicts with the blueprint on behavior or module scope, obey the blueprint.
   - If the codebase conflicts with the blueprint on user-facing behavior, stop and surface the conflict.
   - If the blueprint says `visual-redesign` and `共享壳决策 = bypass`, do not force reuse of the old page shell just because it exists.
4. Map blueprint sections to code.
   - Read [references/pre-code-summary.md](references/pre-code-summary.md).
   - Output the required pre-code summary before touching implementation code.
   - Read [references/implementation-workflow.md](references/implementation-workflow.md).
   - Implement route placement, page shell, module order, component boundaries, states, and business copy from the blueprint.
5. Verify before finishing.
   - Read [references/verification-contract.md](references/verification-contract.md).
   - Read [references/delivery-checklist.md](references/delivery-checklist.md).
   - Run the required hard checks, then check layout drift, missing states, copy drift, and unauthorized module additions.

## Mandatory Rules

- Do not start from the mock alone when a blueprint exists.
- Do not invent modules, routes, filters, actions, or status semantics that are not justified by the blueprint or the codebase.
- Reuse existing components and tokens before creating new ones.
- Respect the blueprint's `改造级别` and `共享壳决策`. Do not silently downgrade a `visual-redesign` into a safe refactor.
- Keep one dominant page mode in implementation, even if the page contains supporting sub-patterns.
- Keep one dominant surface in implementation. Do not let KPI, chart, table, rail, and detail sections compete as co-equals.
- If the blueprint says the redesign breaks the old structure, that break must be visible in the implemented shell, first-screen order, or module hierarchy. A spacing-only or styling-only rewrite does not satisfy the blueprint.
- Implement all required loading, empty, error, disabled, stale, and restricted states from the blueprint.
- Keep business copy aligned with the blueprint unless the user explicitly asks for copy changes.
- Default to visual restraint. Decorative gradients, oversized hero banners, giant soft cards, multi-color badge noise, and dashboard-demo styling are forbidden unless the user explicitly asks for them and the blueprint supports them.
- Route/context realism is mandatory. The implementation must preserve entry points, drill-down paths, and return context defined by the blueprint.
- Respect shell mode exactly. If the blueprint says `workspace shell`, do not quietly re-center the page inside a narrow showcase canvas. If the blueprint says `centered page`, do not wrap it in unnecessary dashboard chrome.

## Visual Rules

- Use the visual reference to match density, hierarchy, alignment, spacing rhythm, and module placement.
- Do not let a pretty mock override blueprint logic.
- If the mock is more detailed than the blueprint, you may borrow harmless visual detail only when it does not create new behavior or scope.
- If the mock is less detailed than the blueprint, finish the missing logic from the blueprint rather than simplifying the page.
- If the blueprint is intentionally structure-first, do not "fill" empty space with extra cards, decorative headers, badge clusters, or analytics chrome.
- When the task is tool-like, prefer professional restraint over visual novelty.

## Engineering Rules

- Map design intent onto the target codebase's existing architecture.
- Prefer composition over one-off page-specific hacks.
- Keep route structure, component ownership, and data boundaries explicit.
- Resolve placement decisions from the codebase first: route files, auth modules, shared UI, page-local components, hooks, and data access should follow the existing project pattern.
- Existing page shells are reusable primitives, not mandatory cages. When the blueprint explicitly calls for `bypass`, keep only the shared parts that still serve the redesign.
- When you add a new component, explain why reuse failed and which blueprint module it serves.
- Treat responsiveness as required implementation work, not a postscript.
- If row comparison matters, do not replace tables with decorative cards.

## Output Rules

- Produce the actual code changes when the user asks for implementation.
- Briefly explain which blueprint sections were implemented, where visual compromises were made, and what remains blocked.
- If blocked by missing codebase context or ambiguous blueprint instructions, stop and ask one focused question instead of improvising.
