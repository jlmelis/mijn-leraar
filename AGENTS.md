# mijn-leraar

Agent skills for creating and driving adaptive, step-by-step build tutorials. The learner builds a real project while learning; progress is tracked in `PROGRESS.md`; the plan adapts in flight.

## Structure

- `skills/` — one directory per skill, each with a `SKILL.md`
  - `leraar-idea` — idea generation + real-function quality gate
  - `leraar-plan` — tutorial creation (tutorial.md + steps + PROGRESS.md)
  - `leraar-guide` — guided build, coach/assistant modes, in-flight adaptation
  - `leraar-verify` — independent verification of step criteria
  - `leraar-plan/assets/templates/` — artifact skeletons (tutorial.md, step.md, progress.md)

## Conventions

- **Skill names:** English words with a `leraar-` prefix (`leraar-idea`, `leraar-plan`, ...).
- **Harness-neutral:** skills must work in any Agent Skills harness (pi, Claude Code, ...). Say "the agent", never a specific product name.
- **Standard frontmatter only:** `name` + `description`. No harness-specific fields.
- **No baked-in technology specifics:** skills never hardcode a language, framework, or package manager. Learners choose; docs are fetched at tutorial-creation time.
- **Docs must be current:** every tutorial records the official docs URL and the date fetched. Never rely on stale memory.
- **Coach by default:** the learner writes the code; skills guide and verify.
- **Templates are the contract:** any change to the PROGRESS.md or step format must update the templates AND all skills that read/write them (plan, guide, verify).

## Working on this repo

- Validate each SKILL.md has a valid `name` + `description` frontmatter before committing (see the validation in the build steps / `pi config` warnings).
- Test changes by running the pipeline on a scratch tutorial in `/tmp` before shipping.
