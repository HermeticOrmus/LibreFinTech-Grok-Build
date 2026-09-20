# LibreFinTech-Grok-Build

**FinTech / payments / compliance skills for [Grok Build](https://github.com/HermeticOrmus/grok-build-reality-os)** — ported and melted from [LibreFinTech-Claude-Code](https://github.com/HermeticOrmus/LibreFinTech-Claude-Code), not a dumb copy.

> Status: **public v0** — three skills melted (`payment-flow-review`, `ledger-design`, `audit-trail`); the rest are honest stubs. See [docs/DEPTH_MATRIX.md](./docs/DEPTH_MATRIX.md).

## Why this exists

Payments and ledgers punish sloppy design. LibreFinTech owns flow review, ledger, KYC/AML checklists, audit trails — melted for Grok Build. Compliance-aware design review; no fraud how-tos. This repo counts only what it has melted.

## Install (<5 min)

See [QUICK_START.md](./QUICK_START.md) for clone, dogfood, project-local, and user-global paths.

```bash
git clone https://github.com/HermeticOrmus/LibreFinTech-Grok-Build.git
cd LibreFinTech-Grok-Build
# Dogfood: .grok/skills/ already has the skill bodies.
# Other project: cp -R skills/* /path/to/your-payments-project/.grok/skills/
```

Doctrine: install [grok-build-reality-os](https://github.com/HermeticOrmus/grok-build-reality-os) `AGENTS.md` on the machine first. Do not replace that doctrine with this pack.

## Depth (honest)

| Artifact | This repo now | Upstream Claude |
|----------|---------------|-----------------|
| Skills | 3 melted + 5 stubs | Proof the job exists; not our inventory |
| Agents | 1 stub (`fintech-orchestrator`) | Proof the job exists; not our inventory |
| Plugins | 1 core bundle stub | Proof the job exists; not our inventory |

Do not paste Claude plugin/agent/command totals here. Update [docs/DEPTH_MATRIX.md](./docs/DEPTH_MATRIX.md) when something melts.

Quality ladder (hygiene, not a badge): this pass targets [L3–L4](https://github.com/HermeticOrmus/grok-build-reality-os/blob/main/docs/QUALITY_LADDER.md). It does not claim L5.

## Skills

| Skill | Status | Job |
|-------|--------|-----|
| payment-flow-review | melted | Authorize/capture/settle/refund — states and idempotency |
| ledger-design | melted | Double-entry sketch: accounts, postings, immutability |
| audit-trail | melted | Who/what/when without leaking secrets or PII |
| kyc-aml-checklist | stub | KYC/AML process checklist (policy framing — not evasion) |
| reconciliation | stub | Daily recon: expected vs actual, breaks, ownership |
| regulatory-map | stub | Map product features to likely regulatory themes |
| fraud-signals | stub | Defensive fraud-signal design — not attack recipes |
| financial-security-defaults | stub | Secure defaults — auth, secrets, least privilege |

Agent: `AGENTS/fintech-orchestrator.md` — stub coordinator for a full suite pass.

## Hard rules

- Documentation and design review only — not legal advice.
- No fraud, evasion, or exploit guidance.
- Never embed real PANs, secrets, or customer PII in examples.

See [SECURITY.md](./SECURITY.md) for how to report issues privately.

## Layout (Grok Build)

```
skills/                 # canonical SKILL.md bodies
AGENTS/                 # suite agents
docs/                   # DEPTH_MATRIX, MELT_RULES
.grok/skills/           # dogfood copy of skills/ (keep in sync)
.grok/plugins/          # optional plugin bundle stub
```

Claude's `.claude/` maps to Grok skills + `AGENTS.md` + `.grok/`. Melt rules: [docs/MELT_RULES.md](./docs/MELT_RULES.md).

## Gold Hat

[GOLD_HAT.md](./GOLD_HAT.md) — empower or extract? Canonical manifesto: [gold-hat-manifesto](https://github.com/HermeticOrmus/gold-hat-manifesto). When a design decision is unclear, choose the option that leaves the user more in control of their own work and their own data.

## Contributing

See [CONTRIBUTING.md](./CONTRIBUTING.md). Melt; do not clone. Honest depth only.

## Suite

- Doctrine: [grok-build-reality-os](https://github.com/HermeticOrmus/grok-build-reality-os)
- This pack: [LibreFinTech-Grok-Build](https://github.com/HermeticOrmus/LibreFinTech-Grok-Build)
- Sibling Libre*-Grok-Build packs: [Arch](https://github.com/HermeticOrmus/LibreArch-Grok-Build) · [Copy](https://github.com/HermeticOrmus/LibreCopy-Grok-Build) · [DevOps](https://github.com/HermeticOrmus/LibreDevOps-Grok-Build) · [Embed](https://github.com/HermeticOrmus/LibreEmbed-Grok-Build) · [FinTech](https://github.com/HermeticOrmus/LibreFinTech-Grok-Build) · [GameDev](https://github.com/HermeticOrmus/LibreGameDev-Grok-Build) · [GEO](https://github.com/HermeticOrmus/LibreGEO-Grok-Build) · [MLOps](https://github.com/HermeticOrmus/LibreMLOps-Grok-Build) · [MobileDev](https://github.com/HermeticOrmus/LibreMobileDev-Grok-Build) · [SecOps](https://github.com/HermeticOrmus/LibreSecOps-Grok-Build) · [SessionFlow](https://github.com/HermeticOrmus/LibreSessionFlow-Grok-Build) · [WhatsApp](https://github.com/HermeticOrmus/LibreWhatsApp-Grok-Build)
- Skills collections: [grok-skills](https://github.com/HermeticOrmus/grok-skills) · [grok-build-skills](https://github.com/HermeticOrmus/grok-build-skills)
- Claude proof: [LibreFinTech-Claude-Code](https://github.com/HermeticOrmus/LibreFinTech-Claude-Code)
- https://ormus.solutions

## License

MIT — see [LICENSE](./LICENSE).
