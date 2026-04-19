# Verification Contract

Use this file to enforce hard checks after implementation.

## Goal

Do not treat visual similarity as sufficient. The page is not done until the relevant repo checks pass or you explicitly report why they could not be run.

## Required Hard Checks

Run the strongest available project-native commands in this order:

1. lint
2. typecheck
3. affected tests or closest relevant test suite
4. build or compile check

If the project exposes one combined verification command, prefer that command when it covers these checks.

## Command Discovery

Before inventing commands, inspect the repo for:

- `package.json` scripts
- monorepo task runners
- framework-specific commands
- existing CI config
- README or contributor docs

Prefer the commands the project already treats as canonical.

## UI-Specific Checks

When the environment allows it, also verify:

- the route renders without crashing
- the dominant modules are visible in the correct order
- loading, empty, error, disabled, stale, and restricted states are not missing
- primary actions and drill-down behavior are wired as intended
- responsive behavior does not collapse the page incorrectly

If browser automation or local runtime is unavailable, say so explicitly.

## Blueprint Conformance Review

After hard checks pass, compare the implementation against the blueprint:

- route intent
- top-level module list and order
- component responsibilities
- required states
- business copy
- visual density and hierarchy

Do not ship if a hard check passes but the page still drifted from the blueprint.

## Failure Handling

- If a hard check fails, fix it before finishing when feasible.
- If you cannot fix it within scope, report the exact failing command and the remaining issue.
- If a hard check is unavailable in the repo, report that absence rather than pretending validation happened.

## Minimum Acceptable Close-Out

A valid implementation close-out should say:

- which commands were run
- which commands passed
- which checks could not be run
- whether the page still has known behavioral or visual drift
