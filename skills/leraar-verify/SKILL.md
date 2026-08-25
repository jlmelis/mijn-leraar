---
name: leraar-verify
description: >
  Independently verifies a learner's work against a step's criteria in a
  leraar-plan tutorial. Reads the actual code and runs the step's verify
  command; reports pass/fail per criterion and updates PROGRESS.md. Use
  when a learner asks "check my work" or before marking a step complete.
---

# Leraar Verify

The examiner. Checks a learner's work honestly against the step's Verify criteria — useful before calling a step done, or any time the learner asks "did I actually get it?"

## Pipeline

```
Idea → leraar-idea → leraar-plan → leraar-guide → leraar-verify (check)
```

leraar-verify can be invoked at any time, independent of leraar-guide: *"check my work on step 4."*

## Workflow

1. **Read the step** — `leraar/steps/NN-*.md` — and its Verify section.
2. **Read PROGRESS.md** for context (what was claimed done, notes).
3. **Check the work — never from memory:**
   - Run the step's verify command yourself (or ask the learner to run it and paste the output).
   - Inspect the actual files the step was supposed to create or change.
4. **Report per criterion**: for each Verify criterion, state pass / fail / partial, quoting the evidence you saw (output, code).
5. **Update PROGRESS.md** only when all criteria pass: mark `[x]` with the commit hash, move `[~]` to the next step, update the date. For partial/fail, leave the step as current and add a Notes line stating exactly what's missing.

## Rules

- **Be honest, be specific.** "Doesn't work" is not a finding; "the verify command exits 1 because <file> is missing" is.
- **Never mark done without evidence.** If you couldn't run the verify command, say so and ask.
- **Coach mode applies** when invoked through the guide: report the gap, don't silently fix it. If the learner asks you to fix it, that's a mode change — confirm first.

## Edge Cases

| Scenario | Behaviour |
|---|---|
| Verify command needs network/paid API | Note it; verify as much as possible offline (imports, syntax, unit tests, dry runs). |
| Learner is on a later step than current | Verify the current step first, then note the gap in PROGRESS.md. |
| Step was skipped | Respect the skip; verify only what the next unskipped step needs. |
| Everything fails | Reassure, list the smallest first fix, suggest the guide split the step. |

## References

- [leraar-guide](../leraar-guide/SKILL.md) — normally drives verification; this skill is the standalone check
- [leraar-plan](../leraar-plan/SKILL.md) — step format (Verify section)
