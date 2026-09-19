# LibreFinTech-Grok-Build

**FinTech / payments / compliance skills for Grok Build** — ported and melted from [LibreFinTech-Claude-Code](https://github.com/HermeticOrmus/LibreFinTech-Claude-Code), not a dumb copy.

> Status: **v0 public scaffold** — honest stubs. Melt depth next.

## Why this exists

Payments and ledgers punish sloppy design. LibreFinTech owns flow review, ledger, KYC/AML checklists, audit trails — melted for Grok Build. Compliance-aware; no fraud how-tos.

## Install (<5 min)

See [QUICK_START.md](./QUICK_START.md).

```bash
mkdir -p .grok/skills
cp -R skills/* .grok/skills/
```

Doctrine: install [grok-build-reality-os](https://github.com/HermeticOrmus/grok-build-reality-os) `AGENTS.md` on the machine first.

## Depth matrix (honest)

| Artifact | v0 scaffold | Upstream Claude (proof) |
|----------|-------------|-------------------------|
| Skills (melted bodies) | 8 stubs → fill next | see upstream suite |
| Agents | 1 (`fintech-orchestrator`) | upstream agents |

Counts on the right are **upstream proof**, not this repo's claim until melted.

## First skills

| Skill | Job |
|-------|-----|
| payment-flow-review | Authorize/capture/settle/refund flow review — states and idempotency |
| ledger-design | Double-entry ledger sketch: accounts, postings, immutability |
| kyc-aml-checklist | KYC/AML process checklist (policy framing — not evasion) |
| audit-trail | Who/what/when audit trail without leaking secrets or PII |
| reconciliation | Daily recon: expected vs actual, breaks, ownership |
| regulatory-map | Map product features to likely regulatory themes (high-level) |
| fraud-signals | Defensive fraud-signal design — detection cues, not attack recipes |
| financial-security-defaults | Secure defaults for FinTech apps — auth, secrets, least privilege |

Agent: `AGENTS/fintech-orchestrator.md` — full suite pass.

## Layout (Grok Build)

```
skills/                 # install into .grok/skills or ~/.grok/skills
AGENTS/                 # suite agents
.grok/plugins/          # optional plugin bundle
docs/                   # DEPTH_MATRIX, MELT_RULES
```

## Gold Hat

[GOLD_HAT.md](./GOLD_HAT.md) — empower or extract?

## Suite

- Doctrine: [grok-build-reality-os](https://github.com/HermeticOrmus/grok-build-reality-os)
- Sibling: [LibreUIUX-Grok-Build](https://github.com/HermeticOrmus/LibreUIUX-Grok-Build) · [LibreSessionFlow-Grok-Build](https://github.com/HermeticOrmus/LibreSessionFlow-Grok-Build) · [LibreGEO-Grok-Build](https://github.com/HermeticOrmus/LibreGEO-Grok-Build)
- Skills packs: [grok-skills](https://github.com/HermeticOrmus/grok-skills) · [grok-build-skills](https://github.com/HermeticOrmus/grok-build-skills)
- Claude proof: [LibreFinTech-Claude-Code](https://github.com/HermeticOrmus/LibreFinTech-Claude-Code)
- https://ormus.solutions

## License

MIT — see [LICENSE](./LICENSE).
