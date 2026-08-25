---
name: leraar-idea
description: >
  Generates real, well-scoped project ideas for learning a technology, in
  any language or stack. Use when a learner wants to build something with
  a technology but has no project in mind, or wants a sanity check that
  their own idea is worth building. Produces a one-file idea brief and
  hands off to leraar-plan. Guarantees the end result is real code with
  real function — never a hello-world or toy demo.
---

# Leraar Idea

Generates project ideas worth learning with. The first step of the mijn-leraar pipeline: a raw learning goal becomes a concrete project that will end in real, usable code.

## Pipeline

```
Idea → leraar-idea (idea brief) → leraar-plan (tutorial) → leraar-guide (guided build) → leraar-verify (check)
```

leraar-idea is optional — a learner who already has a project idea can skip straight to leraar-plan. If invoked with an idea in hand, run a quality-gate check on it instead of generating new ones.

## Workflow

### 1. Gather context (one question at a time)

Ask, one at a time, only what you still need:

- *"How much experience do you have with <tech> (and programming in general)?"*
- *"How much time can you spend per session, and overall?"*
- *"Is there something you'd actually use — a tool for your own workflow?"*

Stop at the minimum. Do not interview the learner.

### 2. Research the technology (current, not remembered)

Before proposing anything:

- Fetch the **official, current documentation** for the technology (web search, curl, or fetch). Record the URL and the date.
- Look at what real projects in that ecosystem actually do (documented examples, popular open-source projects, official tutorials).

If you have no network access, stop and ask the learner for the current official docs URL (or a paste of the relevant pages) before continuing. Never propose ideas from possibly-stale memory.

### 3. Propose 2–3 project ideas

For each idea, state:

- **Concept** — one or two sentences.
- **Why it's real** — who would use it and why it does something non-trivial. It must be something the learner would plausibly use.
- **Scope** — S / M / L with an estimated total time.
- **Concepts it forces you to learn** — the technology's core ideas the learner will hit.
- **Risks** — why it might be too big, too small, or boring.

### 4. Apply the real-function quality gate

Reject or reshape any idea that fails these criteria:

- Has real inputs, outputs, and side effects (reads/writes files, calls an API, serves requests, automates something) — not a static demo.
- Would be useful to the learner (or someone) after the tutorial ends.
- Requires more than one trivial concept of the technology.
- Is achievable in the learner's time budget with room to grow.

"Todo list", "hello world", "counter", and "portfolio" are only acceptable if substantially reimagined into something with real function (e.g. a multi-user todo service with auth, persistence, and tests).

### 5. Produce the idea brief

When the learner picks an idea, write `leraar/idee.md` in the project folder (create the folder if needed):

```markdown
# Idea: <name>

- **Concept:** <one or two sentences>
- **Why it's real:** <who uses it, what it does>
- **Tech:** <technology + versions noted at time of writing>
- **Scope:** S/M/L — <estimated total time>
- **Concepts to learn:** <the technology's core ideas it forces>
- **Risks / scope guardrails:** <what to cut if it grows>
- **Docs checked:** <url + date>
```

Then tell the learner to run `leraar-plan` with this brief.

## Edge Cases

| Scenario | Behaviour |
|---|---|
| Learner already has an idea | Skip generation; run the quality gate on their idea. If it passes, proceed to leraar-plan. If not, reshape it together. |
| Learner wants something "boring" (a script they'll actually use) | Great — small scope is valid if the function is real. |
| Idea is too big | Apply the guardrails: cut features, keep one vertical slice that works end-to-end. |
| No network access | Ask for current docs before proposing anything. |
| Learner can't decide | Recommend the idea with the best ratio of real usefulness to scope fit. |

## References

- [leraar-plan](../leraar-plan/SKILL.md) — downstream; consumes the idea brief
- [leraar-guide](../leraar-guide/SKILL.md) — drives the build
- [leraar-verify](../leraar-verify/SKILL.md) — checks work against criteria
