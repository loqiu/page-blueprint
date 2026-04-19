# Implementation Workflow

Use this sequence to turn a blueprint into code.

## 0. Restate the implementation intent

Before code, output the pre-code summary from `pre-code-summary.md`.

Do not skip this step for implementation work. It is the last chance to catch:

- wrong page mode
- wrong dominant surface
- wrong route context
- decorative drift
- missing real-product states

## 1. Rebuild the page structure

Map the blueprint into:

- route file or route registration
- page shell
- top-level modules in the correct order
- supporting drawers, rails, or detail panels

Ensure the implemented structure still reflects:

- one dominant surface
- clear primary / secondary / supporting regions
- the blueprint's route and context model

Do not start with styling details before the page skeleton is correct.

## 2. Map modules to components

For each blueprint module:

- identify the existing reusable component candidates
- decide whether composition is enough
- create a new component only if reuse would break the blueprint contract

Each implemented module should answer:

- what it renders
- where its data comes from
- what actions it owns
- what states it must cover

## 3. Implement states early

Before polish, ensure every required module can represent:

- loading
- empty
- error
- disabled
- stale or outdated
- restricted, if applicable

Do not leave states as future TODOs unless the user explicitly accepts that gap.

## 4. Sync copy and actions

Implement labels, helper text, status labels, and action text from the blueprint.

Do not replace precise business copy with generic placeholders such as:

- "Item"
- "Details"
- "Action"
- "View more"

unless the blueprint itself uses them.

## 5. Apply visual fidelity

Use the mock or screenshot to tune:

- column widths
- panel balance
- spacing density
- sticky regions
- header emphasis
- row rhythm

Do this after the structural and behavioral mapping is correct.

Do not use this stage to add decorative chrome that weakens the task path.

## 6. Verify responsive behavior

Implement the desktop intent first, then adapt tablet and mobile according to the blueprint.

Do not just shrink the desktop layout.
