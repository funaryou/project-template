---
name: design-direction
description: Define visual direction for a page, feature, or UI refresh in this repository.
license: Proprietary
compatibility: opencode
metadata:
  domain: design
  audience: project
  output: direction
---

## What I do

- Clarify the visual and UX direction for a page or feature
- Translate vague design goals into concrete UI guidance
- Propose a tone, hierarchy, spacing approach, and component feel

## When to use me

Use this skill when:

- a new page needs a visual direction before implementation
- an existing screen feels inconsistent and needs a clearer design target
- the team wants a concrete design brief instead of abstract preferences

Do not use this skill when the main task is bug fixing or code refactoring. In that case, use a future implementation-oriented skill instead.

## Workflow

1. Identify the page goal, primary user action, and content priority.
2. Check relevant project context in `doc/` and current UI assets in `demo/` or `<app-source>/`.
3. Summarize the design problem in one short sentence.
4. Propose a direction across these axes:
   - visual tone
   - information hierarchy
   - layout rhythm
   - typography character
   - color and emphasis usage
5. Note tradeoffs and any assumptions that still need confirmation.

## Output contract

Always structure the response with these headings:

- Goal
- Current problem
- Proposed direction
- Layout guidance
- Typography guidance
- Color guidance
- Risks or open questions

## Project context

- This repository separates human-facing docs in `doc/` from agent-facing instructions in hidden directories.
- Design exploration artifacts currently exist under `demo/design/`.
- The production app is under `<app-source>/`.
- Reuse project-specific principles from `.opencode/resources/design/design-principles.md`.
- Follow output expectations from `.opencode/resources/design/output-contracts.md`.

## Guardrails

- Prefer concrete guidance over vague adjectives.
- Keep proposals implementable in a Next.js app.
- Call out when a proposed direction would require larger component or layout refactors.
- If the current UI already has a strong pattern, evolve it instead of replacing it casually.
