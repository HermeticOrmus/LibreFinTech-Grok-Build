# Contributing

## Melt, don't clone

Ports from LibreFinTech-Claude-Code must follow Liquid Gold:

1. Keep model-agnostic FinTech knowledge (states, invariants, checklists).
2. Strip Claude-only paths, `model:` pins, Anthropic install residue, slash-command theater.
3. Ship as Grok `SKILL.md` / agents under `.grok/` conventions.
4. Teach while helping (Gold Hat).
5. Stay on the compliance / design-review side of the line. No fraud recipes, no evasion, no exploit steps.

## Skill format

```
skills/<name>/SKILL.md
```

YAML frontmatter: `name`, `description`. Body: when to use, steps, measurable checks, worked toy example, output shape.

## PR bar

- Honest depth: only count what you melt. Status is `stub` or `melted` in [docs/DEPTH_MATRIX.md](./docs/DEPTH_MATRIX.md).
- No "Grok killer" language. No Claude plugin/agent/command totals as this repo's inventory.
- Suite footer on README / QUICK_START / AGENTS.md: Reality OS + sibling Libre*-Grok-Build packs.
- Canonical skill body is `skills/<name>/SKILL.md`. Keep `.grok/skills/<name>/SKILL.md` identical.
- No secrets, real PANs, or customer PII in skills, templates, or examples.
- Do not claim a [quality ladder](https://github.com/HermeticOrmus/grok-build-reality-os/blob/main/docs/QUALITY_LADDER.md) rung the tree does not meet.
