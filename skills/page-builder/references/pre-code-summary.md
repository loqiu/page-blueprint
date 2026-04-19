# Pre-Code Summary

Before implementation code, restate the blueprint in this exact structure.

```text
Page Mode:
Primary User Task:
First 10-Second Information Need:
Dominant Surface:
Shell Mode:
Route Position:
Entry / Exit Paths:

Layout Strategy:
- primary region
- secondary region
- supporting region

Key Modules:
- ...
- ...
- ...

Action Placement:
- primary action
- secondary action
- row/contextual action
- destructive action

State Handling:
- loading
- empty
- error
- stale
- permission-restricted

Reuse Plan:
- existing components to reuse
- new components if necessary

Structural Red Lines:
- what must remain dominant
- what must stay secondary
- what old structure must not return
```

## Rules

- Derive this summary from the approved blueprint and the shared design rules, not from taste alone.
- If the blueprint does not support this summary without guessing, stop and clarify before coding.
- Use the summary to prove the page has one dominant mode, one dominant surface, clear route context, real product states, and a justified reuse plan before implementation starts.
