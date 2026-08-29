# mijn-leraar

*Your own teacher* — agent skills that turn any learning goal into an adaptive, step-by-step build tutorial. The tutorial always ends in **real code with real function**, never a hello-world.

## The pipeline

| Skill | Job |
|---|---|
| `leraar-idea` | No project idea? Generates real ones. Quality-gates any idea against "real function". |
| `leraar-plan` | Creates the tutorial: `tutorial.md`, numbered step files (essences — what to build, not the code), `PROGRESS.md` tracker — with current official docs linked and dated. |
| `leraar-guide` | Walks you through step by step, generating each step's code in flight against what you've actually written. Coach mode by default (you type, it teaches); adapts the plan in flight. |
| `leraar-verify` | Honestly checks your work against the step's criteria before you call a step done. |

## Install

### pi

```bash
pi install ./mijn-leraar          # local path
# or
pi install git:github.com/jlmelis/mijn-leraar
```

Then just ask: *"I want to learn smolagents, generate an idea"* — the agent loads `leraar-idea` and the pipeline starts.

### Claude Code / any Agent Skills harness

Skills follow the Agent Skills standard, so nothing special is needed — grab the `skills/` directory and put it on your skills path:

```bash
mkdir -p ~/.claude/skills
ln -s /path/to/mijn-leraar/skills/leraar-* ~/.claude/skills/
```

## A tutorial looks like

```
<learning-project>/
├── leraar/
│   ├── idea.md          # the idea (and why it's real)
│   ├── tutorial.md      # objectives, dated docs, definition of done
│   ├── PROGRESS.md      # the tracker (current step, statuses, notes)
│   └── steps/           # one concept per step (essences — the guide generates the code)
│       ├── 00-setup.md
│       └── ...
├── .gitignore
└── <real code, built step by step>
```

Git history is the backup progress tracker — one commit per step.

## License

MIT
