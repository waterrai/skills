# WaterrAI Skills

Agent skills that teach [Claude Code](https://docs.claude.com/en/docs/claude-code) and [OpenAI Codex](https://openai.com/index/introducing-codex/) how to build on the WaterrAI platform — personas, scenarios, meetings, transcripts, analyses.

Each skill bundles the canonical [WaterrAI developer docs](https://docs.waterr.ai/api-reference/quickstart) as reference material and includes a `generate-understanding` sub-skill that forces a written scope-of-work before any code is written.

## Layout

```
claude/waterr/                              # Claude Code skill
├── SKILL.md                                # Parent skill — docs URLs, resource model, build sequence
└── skills/
    └── generate-understanding/
        └── SKILL.md                        # Nested scoping-interview sub-skill

codex/waterr/                               # Codex equivalent
├── AGENTS.md                               # Always-on project rules
└── prompts/
    └── generate-understanding.md           # @-referenced scoping interview
```

## Install

### Claude Code

```bash
git clone https://github.com/waterrai/skills.git ~/.claude/skills/waterrai
```

Update later:

```bash
cd ~/.claude/skills/waterrai && git pull
```

Full instructions: https://docs.waterr.ai/skills/claude-code

### Codex

From the root of the project where you'll run Codex:

```bash
git clone https://github.com/waterrai/skills.git .waterr-skill
cp -r .waterr-skill/codex/waterr/* ./
```

If you already have an `AGENTS.md`, append rather than overwrite.

Full instructions: https://docs.waterr.ai/skills/codex

## What the skills do

1. When you ask the agent to build something on WaterrAI, the parent skill (`waterr` / `AGENTS.md`) loads.
2. For any non-trivial build, it first runs the nested `generate-understanding` skill: a 3-round structured interview that produces a `WATERR_BUILD_SCOPE.md` file in your project root.
3. You sign off on the scope. *Only then* does the agent write code, citing the docs URL beside every endpoint it calls.

The scoping gate is the whole point — most failed Waterr integrations are scoped wrong, not coded wrong.

## Contributing

PRs welcome. Keep the skill files terse and link to the live docs at https://docs.waterr.ai rather than duplicating content here — the docs are the source of truth.
