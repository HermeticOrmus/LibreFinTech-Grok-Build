# Contributing

## Ways to contribute

- **Seal a crack.** [LEDGER.md](./LEDGER.md) lists the open cracks with their evidence. Pick one, write the seal (a check that fails first, then the fix, then the doc line that now tells the truth), and open a pull request that names the crack ID.
- **Melt a pack skill into a Grok-native one.** The stubs in `stubs/skills/` each name the LibreFinTech-Claude-Code plugin that holds the depth. Melt one into a real Grok skill under `plugins/libre-fintech-grok/skills/` by the rules below.
- **Report a routing miss.** When Grok picks the wrong skill, or none, the description is what needs fixing: [routing miss form](https://github.com/HermeticOrmus/LibreFinTech-Grok-Build/issues/new?template=routing-miss.yml).
- **Propose a plugin.** A payments or ledger job that nothing here covers: [plugin proposal form](https://github.com/HermeticOrmus/LibreFinTech-Grok-Build/issues/new?template=plugin-proposal.yml). General feedback goes in the [feedback form](https://github.com/HermeticOrmus/LibreFinTech-Grok-Build/issues/new?template=feedback.yml).

## Melt, don't clone

Ports from LibreFinTech-Claude-Code must follow Liquid Gold:

1. Keep model-agnostic FinTech knowledge (states, invariants, checklists).
2. Strip Claude-only paths, `model:` pins, Anthropic install residue, slash-command theater.
3. Ship as Grok `SKILL.md` in the `plugins/libre-fintech-grok/` plugin (Grok reads `.grok-plugin/plugin.json`).
4. Teach while helping (Gold Hat).
5. Stay on the compliance / design-review side of the line. No fraud recipes, no evasion, no exploit steps.

## Skill format

```
plugins/libre-fintech-grok/skills/<name>/SKILL.md   # melted skills (installed)
stubs/skills/<name>/SKILL.md                        # stub cues (not installed)
```

YAML frontmatter: `name`, `description` (quote it if it contains `: `). The description is the routing line: say what the skill does and when to use it. Body: when to use, steps, measurable checks, worked toy example, output shape.

When a stub melts: `git mv stubs/skills/<name> plugins/libre-fintech-grok/skills/<name>`, remove its "Stub, not installed" line and the "Stub cue" prefix, and update [docs/DEPTH_MATRIX.md](./docs/DEPTH_MATRIX.md).

The pack entries in `.grok-plugin/marketplace.json` are generated. Run `scripts/pin-pack.sh` to move them to the pack's current commit; do not edit them by hand.

## PR bar

- Honest depth: only count what you melt. Status is `stub` or `melted` in [docs/DEPTH_MATRIX.md](./docs/DEPTH_MATRIX.md).
- No "Grok killer" language. No Claude plugin/agent/command totals as this repo's inventory.
- Suite footer on README / QUICK_START / AGENTS.md: Reality OS + sibling Libre*-Grok-Build packs.
- Canonical skill bodies are `plugins/libre-fintech-grok/skills/<name>/SKILL.md` (melted) and `stubs/skills/<name>/SKILL.md` (stubs). Keep `.grok/skills/<name>/SKILL.md` identical; CI checks it. Links that leave a skill's folder are absolute GitHub URLs, so they still work after install.
- No secrets, real PANs, or customer PII in skills, templates, or examples.
- Do not claim a [quality ladder](https://github.com/HermeticOrmus/grok-build-reality-os/blob/main/docs/QUALITY_LADDER.md) rung the tree does not meet.
