# LibreFinTech-Grok-Build — suite agents

> Ported and melted for **Grok Build**. Not a dumb Claude clone.

**Doctrine hub:** [grok-build-reality-os](https://github.com/HermeticOrmus/grok-build-reality-os) `AGENTS.md`
**Gold filter:** Does this empower or extract? → [GOLD_HAT.md](./GOLD_HAT.md)

## How to use this suite

1. Install skills (see [QUICK_START.md](./QUICK_START.md)).
2. Keep Reality OS as the global doctrine layer.
3. Use suite skills for FinTech; use `AGENTS/fintech-orchestrator.md` when a full pass is needed.

## Agents in this repo

| Agent | File | Role |
|-------|------|------|
| fintech-orchestrator | `AGENTS/fintech-orchestrator.md` | Coordinates payment flow, ledger, KYC/AML checklist, audit, recon, regulatory map into one FinTech pass |

Project-level `AGENTS.md` in a consumer repo wins for project rules; this file is suite guidance. Reality OS `AGENTS.md` wins on doctrine conflicts.

## Liquid Gold

Recognize gold in LibreFinTech-Claude-Code → strip Claude residue → integrate with Grok skills / `.grok/` / MCP → dogfood.

Melted in this pack: `payment-flow-review`, `ledger-design`, `audit-trail`. The other five skills and this orchestrator remain stubs. Honest counts: [docs/DEPTH_MATRIX.md](./docs/DEPTH_MATRIX.md).

## Hard rules

- Documentation and design review only — not legal advice.
- No fraud, evasion, or exploit guidance.
- Never embed real PANs, secrets, or customer PII in examples.

## Suite

- Doctrine: [grok-build-reality-os](https://github.com/HermeticOrmus/grok-build-reality-os)
- This pack: [LibreFinTech-Grok-Build](https://github.com/HermeticOrmus/LibreFinTech-Grok-Build)
- Sibling Libre*-Grok-Build packs: [Arch](https://github.com/HermeticOrmus/LibreArch-Grok-Build) · [Copy](https://github.com/HermeticOrmus/LibreCopy-Grok-Build) · [DevOps](https://github.com/HermeticOrmus/LibreDevOps-Grok-Build) · [Embed](https://github.com/HermeticOrmus/LibreEmbed-Grok-Build) · [FinTech](https://github.com/HermeticOrmus/LibreFinTech-Grok-Build) · [GameDev](https://github.com/HermeticOrmus/LibreGameDev-Grok-Build) · [GEO](https://github.com/HermeticOrmus/LibreGEO-Grok-Build) · [MLOps](https://github.com/HermeticOrmus/LibreMLOps-Grok-Build) · [MobileDev](https://github.com/HermeticOrmus/LibreMobileDev-Grok-Build) · [SecOps](https://github.com/HermeticOrmus/LibreSecOps-Grok-Build) · [SessionFlow](https://github.com/HermeticOrmus/LibreSessionFlow-Grok-Build) · [WhatsApp](https://github.com/HermeticOrmus/LibreWhatsApp-Grok-Build)
- Skills collections: [grok-skills](https://github.com/HermeticOrmus/grok-skills) · [grok-build-skills](https://github.com/HermeticOrmus/grok-build-skills)
- Claude proof: [LibreFinTech-Claude-Code](https://github.com/HermeticOrmus/LibreFinTech-Claude-Code)
- https://ormus.solutions
