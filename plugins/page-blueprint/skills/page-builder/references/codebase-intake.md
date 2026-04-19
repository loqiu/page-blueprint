# Codebase Intake

Read this before implementing anything in a real frontend repository.

If this is the first time touching the repo and the target page is not yet settled, run `../../../shared/guides/project-intake.md` first.

## Goal

Before coding, identify how the target repo already organizes:

- routes and page entry points
- shared layout and app shell
- authentication
- components
- hooks
- data access
- types
- styling and tokens
- tests and verification commands

Do not decide placement from personal preference when the repo already has a pattern.

## First Pass Checklist

Inspect the repo and answer these questions first:

- Which framework and router are in use?
- Where do page or route entry files live?
- Where are shared layout primitives defined?
- Where do reusable UI components live?
- Where do page-specific components usually live?
- How are API calls or server actions organized?
- How is auth wired today?
- Where do types and schemas live?
- Which commands run lint, typecheck, tests, and build?

## Placement Rules

## Routes

- Place new pages where the existing router expects them.
- Follow the current route family and nesting conventions from the codebase.
- Keep route-local modules close to the route unless they are already reused elsewhere.

## Authentication

- Do not invent a new auth layer if the repo already has one.
- Find the current auth entry points first: middleware, session helpers, provider setup, route guards, or `auth.ts` / `auth.js`.
- Put page-specific access checks near the route or loader boundary, not in random UI components.
- If the repo already uses Auth.js or NextAuth conventions, follow the existing file placement exactly instead of introducing a second auth helper.

## Components

- If a component serves only one page, keep it page-local.
- If a component is reused across route families or clearly belongs to the design system, place it in the shared UI area.
- Do not move a page-local component into shared UI just because it might be reused later.
- Do not create a giant `components/` dump with weak ownership.

## Hooks and Data Access

- Keep page-specific hooks near the page or feature module.
- Keep shared hooks only when they are already used across multiple areas or clearly generic.
- Follow the existing API client, fetcher, query, or server-action pattern instead of introducing a parallel one.

## Types and Constants

- Keep page-local view models and constants close to the page.
- Keep domain-wide types where the repo already keeps them.
- Do not push every label or enum into a global constants folder without a real reuse reason.

## Styling

- Use the repo's existing styling system: CSS modules, Tailwind, styled-components, tokens, or utility layers.
- Do not introduce a second styling approach for one page.
- Reuse token access patterns already present in the project.

## Decision Rules

- Blueprint decides behavior and module boundaries.
- Codebase decides file placement and technical integration.
- If the repo has two competing patterns, choose the one closest to the target route family and mention the decision.
- If the repo has no clear pattern, choose the smallest local placement that can grow later without a rewrite.

## Anti-Patterns

- Creating a second auth service when one already exists
- Dumping page-local pieces into shared UI
- Introducing a new state library for one page
- Creating broad "utils" or "helpers" files for page-specific logic
- Hiding placement uncertainty by scattering files across unrelated folders
