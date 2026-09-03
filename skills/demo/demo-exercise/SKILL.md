---
name: demo-exercise
description: Hands-on exercise workflow using base/demo branch separation and INDEX.md navigation. Applicable to any repository.
license: Proprietary
compatibility: opencode
metadata:
  domain: lesson
  audience: general
  output: exercise
---

## What I do

- Design explanations that include hands-on exercises
- Isolate each exercise on its own branch to keep diffs readable
- Manage navigation with INDEX.md on main and on each exercise branch
- Commit and push each exercise unit with a consistent message format

## When to use me

Use this skill when:

- an answer should include an exercise or runnable verification step
- a new trial or explanatory example needs an isolated branch
- an existing exercise needs a deep-dive follow-up
- an exercise index or navigation needs updating

Do not use this skill when the main task is production code fixing, refactoring, or formal document authoring. In that case, use the repository's implementation or documentation workflow instead.

## Variables

Adapt the following variables to the current repository before starting work:

| Variable | Meaning | Example |
|----------|---------|---------|
| `<exercise-area>` | Directory AI may freely create and edit for exercises | `demo/` |
| `<domain>` | Exercise domain or tech area | `servlet` |
| `<topic>` | One-line exercise summary in branch-safe form | `data-equals` |
| `<main-index>` | Index file on main branch | `INDEX.md` |

Confirm these values with the user if they are not already decided. If no instruction exists, use `<exercise-area>=demo/` and `<main-index>=INDEX.md`.

## Workflow

1. Define the exercise theme in one sentence.
2. Confirm `<exercise-area>`, `<domain>`, and `<topic>`.
3. Prepare the branch (Branch rule):
   - Check whether `base/<domain>` exists
   - Branch new exercises from `base/<domain>` as `demo/<domain>/<topic>`
   - Add deep-dives as extra commits on the same `demo/<domain>/<topic>` branch
4. Decide artifact location inside `<exercise-area>`.
5. Respect the repository's `.gitignore`. Never commit build outputs, logs, local databases, or IDE work files unless explicitly instructed.
6. Build and verify in the smallest unit.
7. Commit per exercise unit. Do not combine multiple themes in one commit.
8. Create and update INDEX.md (Index rule):
   - Create the exercise-specific `INDEX.md` on the `demo/<domain>/<topic>` branch
   - Append one row for the exercise to the `INDEX.md` table of contents on `main`
9. Always finish an exercise with commit/push. Push when a remote exists, otherwise finish with a local commit.
10. Report branch name, commit content, and verification steps.

## Branch rule

1. `base/<domain>` is the template for that domain. Do not edit it except for base fixes.
   - Example: `base/servlet`
   - Direct commits are allowed only for base maintenance
2. Branch new exercises from `base/<domain>`. Name the branch `demo/<domain>/<topic>`.
   - Example: `demo/servlet/data-equals`, `demo/servlet/dto-separation`
   - Do not branch from another `demo/` branch
3. Add deep-dives only as extra commits on the same `demo/<domain>/<topic>` branch.
   - Start a new theme from `base/` instead of treating it as a deep-dive
   - Do not merge `demo/` back into `base/`

## Index rule

- `INDEX.md` on `main` is the table of contents. Do not implement exercises on `main`.
- `INDEX.md` on `demo/<domain>/<topic>` is the entry point for that exercise and must explain how to return to `main`.
- Because branch names are fixed, the table can be generated or updated from `git branch --list "base/*" "demo/*"` and commit summaries.

### main-side INDEX.md

- Location: repository root `INDEX.md` (or `<main-index>`)
- Contents:
  1. Domain list
  2. `base/` branch list
  3. `demo/` branch list with branch name, summary, parent `base/`, and checkout command
  4. How to find and switch exercises
- Update timing: append one row when a new `demo/` branch is created
- Example:

```md
# Exercise index

## Demo list

| Branch | Summary | Parent base | Switch |
|--------|---------|-------------|--------|
| demo/servlet/data-equals | Reproduce equals issue | base/servlet | `git switch demo/servlet/data-equals` |
```

### demo-side INDEX.md

- Location: root `INDEX.md` on the `demo/<domain>/<topic>` branch
- Contents:
  1. Purpose and summary of the exercise
  2. Parent `base/` branch name
  3. Run and verification steps
  4. How to return to `main`
- Example:

```md
# demo/servlet/data-equals

- Purpose: reproduce equals issue
- Parent base: base/servlet
- Verify: http://localhost:9090/demo

## Return to main

```bash
git switch main
```
```

## Commit message rule

Use the following uniform format:

```text
demo: <summary of what the exercise shows or explains>
```

- Keep the `demo:` prefix to distinguish exercise work from production changes
- Write one theme per commit
- Optionally add 1-3 lines of learning points or verification steps in the body

Example:

```text
demo: add equals-reproduction exercise

- Compare behavior before and after persistence
- Verify at http://localhost:9090/demo
```

## Guardrails

- Treat `<exercise-area>` as freely usable. Creation and edits there do not require explicit instruction.
- Do not affect areas outside `<exercise-area>` except for the `main` table of contents. Avoid duplicate materials and link by reference where possible.
- Preserve `base/<domain>` as a template. Edit it only for base fixes.
- Always branch `demo/` work from `base/<domain>`. Do not branch from another `demo/` branch.
- Do not merge `demo/` into `base/`.
- Do not implement exercises on `main`. Manage only the `INDEX.md` table of contents there.
- Every `demo/` branch must contain its own `INDEX.md` with a return path to `main`.
- Respect `.gitignore`. Confirm with the user before committing ignored files.
- Keep exercises consistent with the repository's design policy, or explicitly document differences.
- Keep one theme per commit.
- Always finish an exercise with commit/push. Push when a remote exists, otherwise finish with a local commit.
