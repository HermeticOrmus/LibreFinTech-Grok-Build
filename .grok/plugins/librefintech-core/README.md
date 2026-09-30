# librefintech-core (v0 plugin stub, kept as a dogfood copy)

This was the v0 plugin bundle. It had no manifest and no skills, so it bundled nothing: Grok saw it only as a project plugin with one agent, the stub orchestrator. It stays as the dogfood copy of `stubs/agents/fintech-orchestrator.md` (the two files must match; CI checks it).

The installable plugin is now [`plugins/libre-fintech-grok/`](https://github.com/HermeticOrmus/LibreFinTech-Grok-Build/tree/main/plugins/libre-fintech-grok), with its own manifest. Install it with `grok plugin marketplace add HermeticOrmus/LibreFinTech-Grok-Build` and `grok plugin install libre-fintech-grok@libre-fintech-grok`.

The melted skills now live in that plugin's `skills/`; the stubs live in `stubs/skills/`. Dogfood copies of both: `.grok/skills/`.

Melted in this pack: `payment-flow-review`, `ledger-design`, `audit-trail`. The other five skills and `fintech-orchestrator` remain stubs. Honest table: [docs/DEPTH_MATRIX.md](../../../docs/DEPTH_MATRIX.md).

This plugin stub is not required for first run. See [QUICK_START.md](../../../QUICK_START.md).
