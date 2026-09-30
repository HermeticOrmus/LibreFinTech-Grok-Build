<p align="center">
  <img src="https://ormus.solutions/mascot/pixellab_liquid_to_key.gif" alt="LibreFinTech Grok Build" width="128" style="image-rendering: pixelated;" />
</p>

<h1 align="center">LibreFinTech Grok Build</h1>

<p align="center">
  <em>FinTech design review in your Grok Build session: payment, ledger and audit skills melted for Grok, plus the LibreFinTech pack by pinned commit</em>
</p>

<p align="center">
  <a href="https://github.com/HermeticOrmus/LibreFinTech-Grok-Build/stargazers"><img src="https://img.shields.io/github/stars/HermeticOrmus/LibreFinTech-Grok-Build?style=flat-square&color=aa8142" alt="Stars" /></a>
  <a href="https://github.com/HermeticOrmus/LibreFinTech-Grok-Build/blob/main/LICENSE"><img src="https://img.shields.io/github/license/HermeticOrmus/LibreFinTech-Grok-Build?style=flat-square&color=aa8142" alt="License" /></a>
  <a href="https://github.com/HermeticOrmus/LibreFinTech-Grok-Build/commits"><img src="https://img.shields.io/github/last-commit/HermeticOrmus/LibreFinTech-Grok-Build?style=flat-square&color=aa8142" alt="Last Commit" /></a>
  <img src="https://img.shields.io/badge/FinTech-aa8142?style=flat-square&logo=stripe&logoColor=white" alt="FinTech" />
  <img src="https://img.shields.io/badge/Grok_Build-aa8142?style=flat-square&logo=x&logoColor=white" alt="Grok Build" />
</p>

---

**FinTech / payments / compliance skills for [Grok Build](https://github.com/HermeticOrmus/grok-build-reality-os)** — ported and melted from [LibreFinTech-Claude-Code](https://github.com/HermeticOrmus/LibreFinTech-Claude-Code), not a dumb copy.

> Status: **v1.0.0**. The three melted skills (`payment-flow-review`, `ledger-design`, `audit-trail`) install as the `libre-fintech-grok` plugin, and all 21 LibreFinTech-Claude-Code plugins install beside them from the same marketplace, pinned by commit. The five stubs stay in `stubs/` and do not install. See [docs/DEPTH_MATRIX.md](./docs/DEPTH_MATRIX.md) and the [kintsugi ledger](./LEDGER.md).

## Why this exists

Payments and ledgers punish sloppy design. LibreFinTech owns flow review, ledger, KYC/AML checklists, audit trails — melted for Grok Build. Compliance-aware design review; no fraud how-tos. This repo counts only what it has melted.

## Install (<5 min)

See [QUICK_START.md](./QUICK_START.md) for the marketplace, dogfood, and copy paths.

```bash
grok plugin marketplace add HermeticOrmus/LibreFinTech-Grok-Build
grok plugin install libre-fintech-grok@LibreFinTech-Grok-Build
# Any pack plugin, pinned by commit, for example:
grok plugin install payment-processing@LibreFinTech-Grok-Build
grok plugin list
```

[QUICK_START.md](./QUICK_START.md) has a loop that installs every entry.

The pack's optional `libre-fintech-hooks` plugin installs too; whether its hooks fire inside a Grok session is unverified ([LEDGER.md](./LEDGER.md)).

Doctrine: install [grok-build-reality-os](https://github.com/HermeticOrmus/grok-build-reality-os) `AGENTS.md` on the machine first. Do not replace that doctrine with this pack.

## Depth (honest)

| Artifact | This repo now | Installed from the pack |
|----------|---------------|-------------------------|
| Skills | 3 melted, in the `libre-fintech-grok` plugin; 5 stubs in `stubs/skills/`, not installed | The skills inside the 21 pack plugins |
| Agents | 1 stub (`fintech-orchestrator`) in `stubs/agents/`, not installed | A specialist agent in each pack plugin except the hooks plugin |
| Plugins | 1 (`libre-fintech-grok`, v1.0.0) | 21 of 21, pinned by commit in `.grok-plugin/marketplace.json`, including the optional `libre-fintech-hooks` |

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

The melted skills install as the `libre-fintech-grok` plugin. The stubs live in `stubs/skills/` and do not install; each one names the pack plugin that holds the real depth, and [docs/DEPTH_MATRIX.md](./docs/DEPTH_MATRIX.md) maps them all.

Agent: `stubs/agents/fintech-orchestrator.md`, the stub coordinator for a full suite pass. It does not install.

Two names now exist twice: the pack's `ledger-design` plugin has a `ledger-design` skill, and its `audit-trails` plugin has an `/audit-trail` command. Call the Grok-native ones by their qualified names, `libre-fintech-grok:ledger-design` and `libre-fintech-grok:audit-trail` ([LEDGER.md](./LEDGER.md)).

## Hard rules

- Documentation and design review only — not legal advice.
- No fraud, evasion, or exploit guidance.
- Never embed real PANs, secrets, or customer PII in examples.

See [SECURITY.md](./SECURITY.md) for how to report issues privately.

## Layout (Grok Build)

```
.grok-plugin/marketplace.json     # marketplace: the Grok-native plugin, then the pack's plugins by pinned commit
plugins/libre-fintech-grok/       # the Grok-native plugin (manifest in .grok-plugin/plugin.json)
  skills/                         # the melted SKILL.md bodies (canonical)
stubs/skills/                     # stub cues; not installed; each names the pack plugin with the depth
stubs/agents/                     # the stub orchestrator; not installed
scripts/pin-pack.sh               # re-pins the pack entries to the pack's main HEAD
docs/                             # DEPTH_MATRIX, MELT_RULES
LEDGER.md                         # kintsugi ledger: the cracks and their seals
.grok/skills/                     # dogfood copy of the plugin skills and the stubs (CI keeps it in sync)
.grok/plugins/librefintech-core/  # v0 bundle stub, kept as the dogfood copy of the stub orchestrator
```

Claude's `.claude/` maps to Grok skills + `AGENTS.md` + `.grok/`. Melt rules: [docs/MELT_RULES.md](./docs/MELT_RULES.md).

## Gold Hat

[GOLD_HAT.md](./GOLD_HAT.md) — empower or extract? Canonical manifesto: [gold-hat-manifesto](https://github.com/HermeticOrmus/gold-hat-manifesto). When a design decision is unclear, choose the option that leaves the user more in control of their own work and their own data.

## Contributing

See [CONTRIBUTING.md](./CONTRIBUTING.md). Melt; do not clone. Honest depth only.

## Kintsugi ledger

[LEDGER.md](./LEDGER.md) lists every crack found in the v0 edition, the evidence, and the seal this release put on it. Open cracks stay open in plain sight until someone seals them.

## Feedback

Tell us what worked and what is missing: [feedback form](https://github.com/HermeticOrmus/LibreFinTech-Grok-Build/issues/new?template=feedback.yml). Grok picked the wrong skill? [Report a routing miss](https://github.com/HermeticOrmus/LibreFinTech-Grok-Build/issues/new?template=routing-miss.yml). Want a new skill or plugin? [Propose it](https://github.com/HermeticOrmus/LibreFinTech-Grok-Build/issues/new?template=plugin-proposal.yml). Ways to contribute: [CONTRIBUTING.md](./CONTRIBUTING.md).

## Suite

- Doctrine: [grok-build-reality-os](https://github.com/HermeticOrmus/grok-build-reality-os)
- This pack: [LibreFinTech-Grok-Build](https://github.com/HermeticOrmus/LibreFinTech-Grok-Build)
- Sibling Libre*-Grok-Build packs: [Arch](https://github.com/HermeticOrmus/LibreArch-Grok-Build) · [Copy](https://github.com/HermeticOrmus/LibreCopy-Grok-Build) · [DevOps](https://github.com/HermeticOrmus/LibreDevOps-Grok-Build) · [Embed](https://github.com/HermeticOrmus/LibreEmbed-Grok-Build) · [FinTech](https://github.com/HermeticOrmus/LibreFinTech-Grok-Build) · [GameDev](https://github.com/HermeticOrmus/LibreGameDev-Grok-Build) · [GEO](https://github.com/HermeticOrmus/LibreGEO-Grok-Build) · [MLOps](https://github.com/HermeticOrmus/LibreMLOps-Grok-Build) · [MobileDev](https://github.com/HermeticOrmus/LibreMobileDev-Grok-Build) · [SecOps](https://github.com/HermeticOrmus/LibreSecOps-Grok-Build) · [SessionFlow](https://github.com/HermeticOrmus/LibreSessionFlow-Grok-Build) · [WhatsApp](https://github.com/HermeticOrmus/LibreWhatsApp-Grok-Build)
- Skills collections: [grok-skills](https://github.com/HermeticOrmus/grok-skills) · [grok-build-skills](https://github.com/HermeticOrmus/grok-build-skills)
- Claude proof: [LibreFinTech-Claude-Code](https://github.com/HermeticOrmus/LibreFinTech-Claude-Code)
- https://ormus.solutions

## License

MIT — see [LICENSE](./LICENSE).
