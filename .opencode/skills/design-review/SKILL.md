---
name: design-review
description: Review an existing screen or mockup and surface prioritized UX and visual design issues.
license: Proprietary
compatibility: opencode
metadata:
  domain: design
  audience: project
  output: review
---

## What I do

- Review existing UI, mockups, or implemented screens
- Find usability, hierarchy, readability, and consistency issues
- Return practical improvements in priority order

## When to use me

Use this skill when:

- a screen already exists and needs critique
- the team wants a design QA pass before or after implementation
- multiple UI issues exist and they need to be sorted into an actionable order

## Workflow

1. Inspect the target screen, file, mockup, or implementation.
2. Evaluate it using the shared review axes:
   - visual hierarchy
   - grouping
   - readability
   - interaction clarity
   - responsive behavior
   - component reuse potential
3. Identify the highest-impact issues first.
4. Explain why each issue matters and what should change.
5. Separate quick wins from deeper structural changes.

## Output contract

Always structure the response with these headings:

- Scope
- Findings
- Quick wins
- Structural follow-ups
- Open questions

Under `Findings`, order issues by severity and keep each one concrete.

## Project context

- This project documents durable design and architecture decisions in `doc/`.
- Existing UI explorations may live in `demo/design/`.
- Shared project rules live in `.opencode/resources/design/design-principles.md`.
- Shared output expectations live in `.opencode/resources/design/output-contracts.md`.

## Guardrails

- Do not give generic praise-heavy feedback.
- Prioritize findings that affect comprehension, task flow, or implementation consistency.
- Avoid suggesting a total redesign when a targeted improvement will solve the problem.
- If there is not enough context, say what is missing instead of inventing certainty.
