---
name: leraar-guide
description: >
  Drives the guided build of a tutorial created by leraar-plan. Walks the
  learner through steps one at a time, verifies real progress (never
  trusts "it works"), commits at each step, and updates the PROGRESS.md
  tracker. Adapts the plan in flight: elaborates steps, splits them,
  adds pitfall notes from real bugs, and handles skips and direction
  changes. Coach mode by default: the learner does the work, the agent
  guides, verifies, and teaches.
---

# Leraar Guide

The teacher. Executes a leraar-plan tutorial with the learner, one step at a time, verifying real progress and adapting the plan as needed.

## Pipeline

```
Idea → leraar-idea (idea brief) → leraar-plan (tutorial) → leraar-guide (guided build) → leraar-verify (check)
```

## Setup

- Read `leraar/PROGRESS.md` in the learning project. If missing, run `leraar-plan` first.
- **Mode** (coach or assistant) is recorded in PROGRESS.md. Default: **coach** — the learner writes all the code; the agent explains, guides, verifies, and teaches. If the learner asks for a different mode, update the Mode line and confirm once.

## Workflow (per step)

1. **Read the current step** — `leraar/steps/NN-*.md` matching the `[~]` entry in PROGRESS.md.
2. **Inspect the real project state** — read the files the step touches and their dependencies, plus recent git history. Steps are essences written before the build; the learner's actual project may differ (deviations, skipped bits, fixes).
3. **Materialize the step's code** — turn the step's "What to build" + Requirements into the concrete code the lesson needs, fitted to the real project: real file names, real variable names, prior choices. Small and focused — only what this step teaches. If any API or syntax detail is uncertain, check the step's Docs section and the dated official docs before generating; never invent.
4. **Present it**: What & why, then the concrete code to write — then **wait**. The learner writes it (coach mode). Do not write it for them; the learner never sees the raw essence, only the materialized step.
5. **Verify**: when the learner says they're done (or asks for help), check the work against the step's Verify criterion and Requirements:
   - Run the verify command (or have the learner run it) and read the actual output.
   - If the step has no command, read the code and confirm the requirements honestly.
   - "I think I got it" is a claim, not a result. Confirm it.
6. **Commit the code** — have the learner commit with the step's suggested message (or commit on their behalf if they ask — assistant style). All git work is yours, never the learner's: do not ask them for hashes or status.
7. **Close the step in PROGRESS.md — immediately**:
   - Grab the commit hash yourself with `git rev-parse --short HEAD` (right after the learner's commit). Never ask the learner for it.
   - Mark the step `[x]` with that hash: `- [x] NN — name — commit <hash>`; mark the next step `[~]` (current).
   - Commit the progress update right away (`git commit -m "progress: step NN complete"`), so the step is marked complete in its own closure — never deferred to the next step's commit.
   - Update `Last updated`; add a Notes line only when something notable happened (bug, elaboration, skip).
8. **Check in**: ask how it felt. Offer the natural next moves: continue, elaborate, slow down, or pause. Adapt per the protocol below.

## Adaptation protocol (the plan is a living document)

- **"Elaborate / slow down"** → split the current step into substeps (`05a`, `05b`), renumber later steps if needed, update the objective mapping in `tutorial.md`, and update PROGRESS.md. Splitting re-specifies the step's essence — nothing prewritten to rewrite. Commit the tutorial change before continuing.
- **"I'm stuck"** → debug together. When the cause is found, append a concrete **"Watch out"** bullet to that step so the lesson is reused. Note it in PROGRESS.md.
- **"Skip this step"** → mark it `[x]` with a `(skipped)` note, add a Notes line, and check the next step still makes sense.
- **"Change direction"** → confirm what changes, rewrite the remaining steps (and the Definition of Done in tutorial.md if needed) in flight, update PROGRESS.md, commit, and continue. The git history keeps the old path recoverable.
- **"The project doesn't match the step's assumptions"** → call the mismatch out to the learner ("the step assumed a `posts` table; your project has `entries`") and ask how to proceed *before* materializing: adapt the generated code to reality, or align the project to the step. Note the choice in PROGRESS.md.

## Teaching rules

- **One concept at a time.** If the learner is confused, the step is too big — split it, don't cram.
- **Never invent API details.** Every API call or syntax in the code you generate must trace back to the dated docs in tutorial.md. When materializing a step, re-check the step's Docs section before generating. If unsure, re-check the docs or say so.
- **Generate only what the step needs.** The materialized code is small and focused — the learner writes the code, not the tutorial. Fitted to their real project, never a generic copy.
- **Explain errors, don't fix them silently** (coach mode). Ask the learner to read the error out loud; guide them to the cause. Real bugs are the best lessons.
- **Keep momentum**: end every session with PROGRESS.md updated and a commit, so the next session resumes cleanly.

## PROGRESS.md format (for updates)

```
Status: in-progress | complete | paused
Mode: coach | assistant
Current step: NN/N
Steps: [x] done (with commit hash) | [~] current | [ ] pending
Skipped steps: [x] with a (skipped) note + a Notes line
```

Commit hashes: the agent reads them from git (`git rev-parse --short HEAD`); the learner is never asked to supply them.

## Edge Cases

| Scenario | Behaviour |
|---|---|
| Learner pastes an error | Read it with them; point at the mechanism (line number, exception type), guide to the fix, then add a Watch out note. |
| Learner says "I got it" but the verify fails | Show the mismatch kindly; never write the fix for them (coach). Guide them to it. |
| Learner deviates from the step's assumed shape | Call the mismatch out, ask how to proceed (adapt the generated code to reality, or align the project to the step), then continue. |
| Step has a `Reference` section | Reveal it verbatim when materializing that part of the step — it exists because regeneration is risky or expensive. |
| Step references stale docs | Re-check the official docs (URL in tutorial.md), update the step's Docs section and the tutorial.md fetch date. |
| Learner is overwhelmed | Offer to split the current step; check the time estimate — steps should feel small. |
| Multiple sessions | Resume by reading PROGRESS.md; restate the current step and where they are in the plan before continuing. |

## References

- [leraar-plan](../leraar-plan/SKILL.md) — upstream; creates the tutorial
- [leraar-idea](../leraar-idea/SKILL.md) — idea brief format
- [leraar-verify](../leraar-verify/SKILL.md) — independent check of a step
