# Quality Gates

Run this checklist before you present a page blueprint.

## Logic

- Can the page goal be stated in one sentence?
- Is there exactly one dominant page mode?
- Does each major module serve the primary task?
- Does the route logic match the business object or workflow step?
- Is the chosen shell mode (`workspace shell` or `centered page`) justified by task posture, density, and application context?

## Scope Control

- Did you avoid fallback, downgrade, compatibility, or patch-style branches?
- Did you avoid adding modules the user did not ask for?
- Are assumptions clearly separated from facts?
- Does the stated `改造级别` match what the user actually asked for?
- Did you choose the correct concrete blueprint template for that `改造级别`?
- For `visual-redesign`, did you define the optimization standard before writing the new structure?
- For `visual-redesign`, if you delete visual or tone adjectives, does the old-vs-new structural difference still stand?

## Component Discipline

- Did you reuse existing patterns before adding new components?
- Does every new component include a reason, responsibility, and state set?
- Are components defined as contracts rather than visual fragments?

## Implementation Handoff

- If the blueprint is repo-backed, does `实现附录` map the page to concrete files, components, stores, composables, or API modules?
- Does the appendix separate page-local work from shared reuse clearly enough for a builder to place code without guessing?
- Are data ownership, state ownership, and verification targets explicit instead of implied?
- If the page uses a shared shell today, does the appendix explicitly say whether the builder should `reuse`, `variant`, or `bypass` that shell?
- Does the appendix state the intended shell mode clearly enough that a builder will not fall back to a centered canvas by habit?

## State Coverage

- Are loading, empty, error, and disabled states covered?
- If the page cares about freshness, permissions, or auditability, are those states covered explicitly?
- Are state treatments attached to real modules instead of vague page-level slogans?

## Copy Quality

- Are page title, actions, and state messages written in business language?
- Is terminology stable across sections?
- Does every empty or error message tell the user what happened and what to do next?

## Output Quality

- Does the document follow the exact section order from the concrete template selected by `改造级别`?
- Is every `待确认` item a real unknown rather than a skipped decision?
- Could a designer or engineer implement the page from this blueprint without asking what each module is for?
- Could a builder start implementation without first asking where the page file, supporting components, and required validations should live?
- For `safe-refactor`, does the document make the preservation boundaries explicit before discussing changes?
- For `visual-redesign`, does the document prove what old structure is being broken and what new reading path replaces it?
- For `visual-redesign`, does the document explain why this new structure is better according to the stated optimization standard, instead of by taste alone?
