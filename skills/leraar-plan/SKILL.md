---
name: leraar-plan
description: >
  Creates a step-by-step build tutorial from a project idea. Turns an idea
  brief (or the learner's own idea) into a tutorial folder with a
  tutorial.md overview, numbered step files, and a PROGRESS.md tracker.
  Each step has a single concept, a verify check, and a commit. Always
  references current official documentation. Works for any technology or
  language; never assumes a specific stack or package manager.
---

# Leraar Plan

Turns a project idea into an adaptive, step-by-step build tutorial. The tutorial is a living document: small steps, verified at each stage, with git as the safety net.

## Pipeline

```
Idea → leraar-idea (idea brief) → leraar-plan (tutorial) → leraar-guide (guided build) → leraar-verify (check)
```

Input: an idea brief (`leraar/idea.md`), or the learner's own idea.
Output: a tutorial folder inside the learning project.

## Setup

- No external dependencies.
- The learning project folder should exist (create it if not).
- **Ask the learner** which toolchain they want (package manager, language version, test framework). Never assume.

## Artifact format

Create inside the learning project:

```
<learning-project>/
├── leraar/
│   ├── idea.md           # idea brief (if from leraar-idea)
│   ├── tutorial.md       # overview, objectives, dated docs, DoD
│   ├── PROGRESS.md       # tracker
│   └── steps/
│       ├── 00-setup.md
│       ├── 01-<name>.md
│       └── ...
```

Copy the skeletons from `assets/templates/` (tutorial.md, step.md, progress.md) and fill them in per the rules below.

## Workflow

### 1. Fetch current official documentation

- Web search / curl / fetch the **official docs** for the technology.
- Record the **URL(s) and the date fetched** in `tutorial.md`.
- If no network access, ask the learner for the current official docs URL or a paste of the relevant pages. Do not proceed on stale memory.

### 2. Scaffold the project

- `git init` (if not already a repo) and create a `.gitignore` appropriate to the chosen toolchain (ask the learner or check the docs).
- Initialize the project with the learner's chosen toolchain **as step 00** — the setup step is itself the first step of the tutorial.

### 3. Write `tutorial.md`

From the template. Required sections:

- **Why this project (not hello world)** — the real function and who uses it.
- **What you'll learn** — objectives, each mapped to step numbers.
- **Tech stack & why** — with the version noted at creation time.
- **Official documentation** — URLs + fetch date. If a step feels stale later, this is where to re-check.
- **Definition of done** — the concrete end state: "the learner can run it and use it for <real purpose>".

### 4. Write the steps

From the step template. Rules:

- **One concept per step.** If a step needs more than one new concept, split it.
- **Small steps.** The "Do" section guidance is roughly 10 lines max — the learner writes the code, not the tutorial.
- **Every step ends with Verify and Commit.** A step that can't be verified or committed is too big; split it.
- Steps are numbered `00-setup`, `01-...`, up to a final step whose Verify criterion is the Definition of Done.
- **Seed 1–3 likely pitfalls** into each step's "Watch out" section. They will grow as learners hit real bugs.

### 5. Write `PROGRESS.md`

From the template. Status: `in-progress`; mode: `coach` by default. Mark step 00 as the current step (`[~]`).

### 6. Commit the scaffolding

One commit: the initialized project plus the `leraar/` folder.

## Why these rules exist

- Small verified steps catch problems early and keep motivation high.
- Committing after each step means git history is a progress tracker and a safety net: the learner can always see where they are and roll back.
- The final step must deliver the Definition of Done — the tutorial ends when the learner has something real, not when the step list runs out.

## Edge Cases

| Scenario | Behaviour |
|---|---|
| Learner has their own idea, no brief | Accept it. Run the real-function quality gate (see leraar-idea) and reshape if needed before planning. |
| Docs are version-specific or paywalled | Note the exact version in tutorial.md, link what's public, flag it in PROGRESS.md notes. |
| Learner wants to skip setup | Skip step 00's actions but keep the step; note the chosen toolchain in tutorial.md. |
| Step list gets long (> ~12 steps) | Check for steps that can be merged without merging concepts. |

## References

- [leraar-idea](../leraar-idea/SKILL.md) — upstream; produces the idea brief
- [leraar-guide](../leraar-guide/SKILL.md) — executes this tutorial
- [leraar-verify](../leraar-verify/SKILL.md) — checks work against steps
