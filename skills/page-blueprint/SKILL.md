---
name: page-blueprint
description: Draft implementation-ready frontend page blueprints from product goals, design rules, screenshots, and repo context. Use when Codex needs to inspect a UI repo, choose page mode and shell mode, define route/context/state behavior, and produce a reviewable page plan before coding.
---

Turn scattered page goals and design rules into one reviewable page blueprint document. Produce documentation first, not implementation code, unless the user explicitly asks for code after the blueprint is agreed.

## Workflow

1. If this is the first contact with a repo, inspect the project first.
   - Read `../../shared/guides/project-intake.md`.
   - If the user only provides a project path or asks where to start, inspect the repo structure before choosing a target page.
   - If there is no UI repo, skip repo intake and treat the task as a greenfield blueprint request.
2. Clarify the target page.
   - Identify the page name, core entity, primary user, primary task, and success condition.
   - If the page objective, core entity, or primary action is unclear and a wrong assumption would distort the blueprint, stop and ask a concise question.
3. Gather evidence in this order.
   - Page-specific source materials: PRD, screenshots, tables, fields, APIs, current routes, business docs.
   - In-repo design rules: always read `../../shared/design/global/Global-Design.md`, `../../shared/design/global/DESIGN-AGENTS.md`, `../../shared/guides/professional-page-generation.md`, and `../../shared/guides/shell-mode-reference.md` first, then read exactly one matching page-mode document from `../../shared/design/page-modes/`.
   - Existing IA, route, component, and copy conventions.
4. Classify the page before drafting.
   - Choose exactly one dominant page mode: `overview dashboard`, `monitoring dashboard`, `operations dashboard`, `detail page`, `browse/discovery page`, or `settings/admin page`.
   - State the dominant user task.
   - State the dominant surface: KPI, chart, table/list, or detail section.
   - Decide `页面壳模式` before writing the blueprint: `workspace shell` or `centered page`.
   - Decide `改造级别` before writing the blueprint: `safe-refactor` or `visual-redesign`.
   - Decide `共享壳决策` before writing the blueprint when the current page already sits in a reusable shell: `reuse`, `variant`, or `bypass`.
   - If `页面壳模式` is unclear and the choice would materially change density, navigation placement, or scroll behavior, stop and ask the user which shell they want.
   - If `改造级别 = visual-redesign`, define the optimization standard before designing the new structure.
   - If `改造级别 = visual-redesign`, write a compact `旧结构骨架` and `新结构骨架` before drafting the full document. Each skeleton must state only route/shell, dominant surface, first-screen order, and top-level modules.
   - If the user did not provide that standard explicitly, derive it from the page goal, user task, existing page problems, and design sources, then mark derived parts clearly as assumptions.
5. Draft the blueprint.
   - Always read [references/output-template.md](references/output-template.md) first, then open exactly one concrete blueprint template based on `改造级别`.
   - Use [references/output-template-safe-refactor.md](references/output-template-safe-refactor.md) for `safe-refactor`.
   - Use [references/output-template-visual-redesign.md](references/output-template-visual-redesign.md) for `visual-redesign`.
   - Read [references/page-mode-reference.md](references/page-mode-reference.md) only to classify the page quickly before opening the full matching design source.
   - Read [references/page-input-contract.md](references/page-input-contract.md) when inputs are incomplete.
   - For repo-backed pages, fill `实现附录` with concrete implementation handoff details for the builder.
   - Read [references/quality-gates.md](references/quality-gates.md) before finalizing.
6. Validate the document.
   - Remove invented business facts.
   - Mark unresolved items as `待确认`.
   - Ensure every module, action, and state has a reason tied to the user task.

## Mandatory Rules

- Follow first principles. Do not jump from vague goals to detailed UI structure without proving the reasoning chain.
- Prefer the shortest correct path. Do not add fallback flows, compatibility branches, or speculative modules unless the user explicitly asks for them.
- Treat the in-repo design docs under `../../shared/design/` as the source of truth. Use this skill's other references as structure and fallback, not as a replacement for those design rules.
- Treat `../../shared/guides/professional-page-generation.md` as a hard constraint for dominant surface discipline, hierarchy, density, route/context realism, table-vs-card decisions, state coverage, and anti-pattern avoidance.
- Treat `../../shared/guides/shell-mode-reference.md` as the source of truth for `workspace shell` vs `centered page`.
- Read exactly one dominant page-mode source per page unless the user explicitly asks for cross-mode comparison.
- Do not invent route names, status models, permission rules, or destructive actions without evidence.
- Keep one dominant page mode. Secondary patterns may support it, but may not redefine the page.
- Treat `页面壳模式` as a structural decision, not as a styling note. `workspace shell` means app-level left rail or utility chrome with fluid content width; `centered page` means page-level canvas inside a bounded content area.
- Keep the blueprint implementation-ready. Every section should help a designer, PM, or engineer make a concrete decision.
- Do not treat `改造级别` as a label only. It must change the blueprint structure itself.
- `safe-refactor` blueprints must preserve and optimize the existing page logic.
- `visual-redesign` blueprints must explicitly redefine the reading path, module hierarchy, and shell strategy instead of merely enlarging or restyling the old structure.
- For `visual-redesign`, the document must first prove the old-vs-new structural difference in route/shell, dominant surface, first-screen order, or top-level module hierarchy. If the difference exists only in styling words, the redesign is invalid.
- For `visual-redesign`, define the optimization criteria first. The new page structure must be traceable back to those criteria instead of to taste alone.
- The optimization criteria must answer at minimum:
  - what the user must understand first,
  - what becomes the dominant stage,
  - which old structure must be broken,
  - what must not be sacrificed while improving the page.
- If visual tone is mentioned, it must be expressed as an effect on hierarchy, density, action clarity, or task posture. Do not use adjectives such as "more modern", "more polished", or "stronger visual impact" as redesign evidence.

## Route Rules

- Design the route from information architecture, not from widget layout.
- Keep route naming centered on the business object or workflow step.
- Define entry points, sibling pages, and drill-down or return paths.
- If the route family is unknown, propose one candidate and label it as an assumption.

## Component Rules

- Reuse existing component patterns before proposing new ones.
- When proposing a new component, explain:
  - why existing patterns are insufficient,
  - which page mode it belongs to,
  - what states or variants it needs,
  - which global rules it depends on.
- Define components as contracts, not screenshots. Include responsibilities, composition, key props or fields, and interaction boundaries.

## Copy Rules

- Use business language, not marketing language.
- Make labels action-first and unambiguous.
- Write copy for normal, empty, error, loading, stale, and restricted states when relevant.
- Keep terminology stable across the whole page.

## Output Rules

- Emit the document in the exact section order from the concrete blueprint template selected by `改造级别`.
- Separate facts, assumptions, and open questions.
- Use concise prose and dense bullets. Avoid filler.
- For repo-backed blueprints, make `实现附录` concrete enough that a builder can place files and wire states without inventing ownership.
- Do not generate code unless the user explicitly asks for the implementation step.
