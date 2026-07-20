---
name: design-implementation-brief
description: Convert design intent or review feedback into an implementation-ready UI brief for this project.
license: Proprietary
compatibility: opencode
metadata:
  domain: design
  audience: project
  output: implementation-brief
---

## What I do

- Translate design ideas into implementation-ready guidance
- Bridge visual intent with component structure and responsive behavior
- Reduce ambiguity before UI coding starts

## When to use me

Use this skill when:

- a design direction is ready and needs to become implementation work
- design review findings need to be turned into concrete UI tasks
- a page should be broken into sections, states, and component boundaries

## Workflow

1. Read the source material:
   - design notes
   - current UI
   - relevant docs
2. Define the exact scope of the page or component.
3. Break the UI into sections and reusable component candidates.
4. List required states, empty states, error states, and responsive changes.
5. Suggest an implementation order that reduces rework.
6. Call out decisions that need product or design confirmation before coding.

## Output contract

Always structure the response with these headings:

- Scope
- UI sections
- States and edge cases
- Responsive rules
- Suggested component boundaries
- Suggested implementation order
- Decisions to confirm

## Project context

- The main application lives in `<app-source>/`.
- Existing design references may live in `demo/design/`.
- Human-readable architecture decisions belong in `doc/`.
- Reuse shared rules from `.opencode/resources/design/design-principles.md`.
- Reuse shared output expectations from `.opencode/resources/design/output-contracts.md`.

## Guardrails

- Make the brief specific enough that an implementation agent can act on it.
- Prefer reusable component boundaries over one-off page-only markup.
- Mention responsive behavior explicitly; do not leave it implied.
- If the design intent conflicts with existing project structure, call that out clearly.
