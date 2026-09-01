# Step NN — <name>
**Time:** ~<n> min (delivered in small rounds — see Build-up) | **One concept:** <single concept>

## What & why
<one concept, in real-world terms, tied to the end goal>

## What to build
<the essence — prose spec of exactly what code this step introduces, precise enough that an agent can write it without seeing it. Name the files to create/modify and what belongs in each, the behavior and data flow, and the specific techniques or APIs to use. NO literal code here: the guide generates it in flight, fitted to what the learner has actually written.

Structure it like a real project, not a script dump: split files along conceptual boundaries — role, responsibility, why a thing changes — never by line count. A file holding one coherent idea is fine at any size; a file holding unrelated ideas should be split even when small. Keep the entry point thin; long constants, prompts, and payloads live in their own module. The step stays one concept whatever its size — the Build-up section below is what keeps it typeable.>

## Build-up
<the ordered ladder the guide presents — one small piece at a time, waiting after each. A piece is a chunk (a few lines), a method (a chunk wrapped in a function), or a file section (related methods grouped into a module) — chunk → method → file. Every piece ends in something checkable — a test, an import, a run — and stays under ~15–20 lines. If a piece can't stay small, break it into more pieces — the ladder, not the step size, is what keeps typing manageable.>
1. <piece: what it is, where it goes, how it's checked — e.g. "has_won(state) in main.py, ~6 lines; check: pytest test passes">
2. <piece: ...>

## Requirements
<the pedagogical contract — checkboxes the guide must satisfy when generating and verifying. Include must-demonstrate techniques ("must use X, not Y"), required behaviors, and modularity (which file holds what).>
- [ ] <technique/API that must be demonstrated>
- [ ] <behavior the step must produce>
- [ ] <edge case that must be handled>
- [ ] <modularity: what lives in its own file/module>

## Verify
<concrete command(s) or check that proves the step worked — runnable without the step's code, so leraar-verify can judge independently>

## Commit
<short commit message>

## Docs
- <section of the official docs (linked in tutorial.md) — the guide re-checks these when materializing the code>

## Watch out
- <likely pitfall 1>
- <likely pitfall 2>

## Reference (optional — last resort)
<only code that is risky or expensive to regenerate: tricky regexes, exact foreign API shapes, known-good config. Revealed verbatim by the guide. Omit this section entirely when the guide can safely generate everything.>
