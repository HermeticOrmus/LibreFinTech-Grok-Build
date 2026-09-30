# Quick Start — LibreFinTech for Grok Build

> From a clean machine to one payments/compliance review cue in under 5 minutes.

Doctrine first: put [grok-build-reality-os](https://github.com/HermeticOrmus/grok-build-reality-os) `AGENTS.md` on the machine (global Grok doctrine). This pack does not replace it.

## Prerequisites

- Grok Build installed: `curl -fsSL https://x.ai/cli/install.sh | bash`, then `grok --version`. Plugin commands need no login.
- `git` (only for the dogfood and copy paths); `jq` for the install-everything loop
- A payments or ledger system you **own** or are **authorized** to review, **or** this repo as the working tree

## Layout this file assumes

Verified against this repository (do not invent extra folders):

```
.grok-plugin/marketplace.json                      # the marketplace: libre-fintech-grok, then the pack's plugins by pinned commit
plugins/libre-fintech-grok/.grok-plugin/plugin.json
plugins/libre-fintech-grok/skills/<name>/SKILL.md  # the melted skills (canonical)
stubs/skills/<name>/SKILL.md                       # stub cues; not installed
stubs/agents/fintech-orchestrator.md               # stub coordinator; not installed
docs/DEPTH_MATRIX.md
docs/MELT_RULES.md
.grok/skills/<name>/SKILL.md                       # dogfood copy; must match its source above
.grok/plugins/librefintech-core/                   # v0 bundle stub; dogfood copy of the stub orchestrator
```

Melted (usable now): `plugins/libre-fintech-grok/skills/payment-flow-review/SKILL.md`, `plugins/libre-fintech-grok/skills/ledger-design/SKILL.md`, `plugins/libre-fintech-grok/skills/audit-trail/SKILL.md`.
Still stubs, in `stubs/`: `kyc-aml-checklist`, `reconciliation`, `regulatory-map`, `fraud-signals`, `financial-security-defaults`, plus the orchestrator. Each stub names the pack plugin with the real depth. Honest table: [docs/DEPTH_MATRIX.md](./docs/DEPTH_MATRIX.md).

## Install (pick one)

### A. Marketplace (recommended)

One marketplace brings the Grok-native plugin and every LibreFinTech-Claude-Code plugin, each pinned to a commit:

```bash
grok plugin marketplace add HermeticOrmus/LibreFinTech-Grok-Build
grok plugin install libre-fintech-grok@LibreFinTech-Grok-Build
grok plugin install payment-processing@LibreFinTech-Grok-Build
```

Grok registers a marketplace added from GitHub under the repo's name, so the part after `@` is `LibreFinTech-Grok-Build`, not the manifest name `libre-fintech-grok`. A bare plugin name also works when no other marketplace you added has a plugin by that name.

Every entry at once (needs `jq`):

```bash
for p in $(curl -fsSL https://raw.githubusercontent.com/HermeticOrmus/LibreFinTech-Grok-Build/main/.grok-plugin/marketplace.json | jq -r '.plugins[].name'); do
  grok plugin install "$p@LibreFinTech-Grok-Build"
done
```

Confirm what landed:

```bash
grok plugin list
grok plugin details libre-fintech-grok
```

You should see `libre-fintech-grok` (three skills: `payment-flow-review`, `ledger-design`, `audit-trail`) plus the pack plugins you installed. The optional `libre-fintech-hooks` plugin installs its hooks, but whether they fire inside a Grok session is unverified ([LEDGER.md](./LEDGER.md)).

Only the Grok-native plugin, without the marketplace:

```bash
grok plugin install HermeticOrmus/LibreFinTech-Grok-Build#plugins/libre-fintech-grok
```

Do not install the repo root itself (`grok plugin install HermeticOrmus/LibreFinTech-Grok-Build`): since v1.0.0 the root holds no skills, so Grok installs an empty plugin.

### B. Dogfood this repo

```bash
git clone https://github.com/HermeticOrmus/LibreFinTech-Grok-Build.git
cd LibreFinTech-Grok-Build
# Dogfood copies of the melted skills and the stubs are at .grok/skills/; open this folder in Grok Build.
```

### C. Install into your payments project (copy, no plugin manager)

```bash
git clone https://github.com/HermeticOrmus/LibreFinTech-Grok-Build.git ~/LibreFinTech-Grok-Build
cd /path/to/your-payments-project
mkdir -p .grok/skills
cp -R ~/LibreFinTech-Grok-Build/plugins/libre-fintech-grok/skills/* .grok/skills/
```

Confirm the copy landed:

```bash
test -f .grok/skills/payment-flow-review/SKILL.md
test -f .grok/skills/ledger-design/SKILL.md
test -f .grok/skills/audit-trail/SKILL.md
ls .grok/skills
```

You should see three skill directories, matching `plugins/libre-fintech-grok/skills/` in this repo. The stubs are not copied: they are cues, not skills.

### D. User-global copy

```bash
git clone https://github.com/HermeticOrmus/LibreFinTech-Grok-Build.git ~/LibreFinTech-Grok-Build
mkdir -p ~/.grok/skills
cp -R ~/LibreFinTech-Grok-Build/plugins/libre-fintech-grok/skills/* ~/.grok/skills/
```

Same three `test -f` checks as C, under `~/.grok/skills/`.

Copy `stubs/agents/fintech-orchestrator.md` only when you want a multi-skill pass. It is still a stub coordinator, and no install path ships it. Merge into existing project `AGENTS.md` / `.grok/AGENTS.md`; do not overwrite Reality OS doctrine.

## First-run teach cue

In Grok Build, on a flow you own (toy amounts, no real PAN or customer PII):

1. **Flow** — "Run payment-flow-review on authorize → capture → settle → refund. Name the money job first. Flag missing idempotency."
2. **Ledger** — "Run ledger-design for that capture: double-entry legs, integer minor units, immutability."
3. **Audit** — "Run audit-trail for who approved a refund — actor, object, time — without logging secrets or PII."

You used melted LibreFinTech depth on Grok — not a Claude paste, not a fake agent count.

## Hard rules

- Documentation and design review only — not legal advice.
- No fraud, evasion, or exploit guidance.
- Never embed real PANs, secrets, or customer PII in examples.

## Smoke checklist

- [ ] `grok plugin list` shows `libre-fintech-grok` (or the three skill files exist at the copy path you chose)
- [ ] Grok can see those three skills
- [ ] One flow review returned severity-ranked findings and remediations (no `/10` score)
- [ ] One ledger sketch balanced in minor units
- [ ] One audit shape named actor + object + time with a never-log list
- [ ] No secrets, PANs, or customer PII in prompts, examples, or output

## Suite

- Doctrine: [grok-build-reality-os](https://github.com/HermeticOrmus/grok-build-reality-os)
- This pack: [LibreFinTech-Grok-Build](https://github.com/HermeticOrmus/LibreFinTech-Grok-Build)
- Sibling Libre*-Grok-Build packs: [Arch](https://github.com/HermeticOrmus/LibreArch-Grok-Build) · [Copy](https://github.com/HermeticOrmus/LibreCopy-Grok-Build) · [DevOps](https://github.com/HermeticOrmus/LibreDevOps-Grok-Build) · [Embed](https://github.com/HermeticOrmus/LibreEmbed-Grok-Build) · [FinTech](https://github.com/HermeticOrmus/LibreFinTech-Grok-Build) · [GameDev](https://github.com/HermeticOrmus/LibreGameDev-Grok-Build) · [GEO](https://github.com/HermeticOrmus/LibreGEO-Grok-Build) · [MLOps](https://github.com/HermeticOrmus/LibreMLOps-Grok-Build) · [MobileDev](https://github.com/HermeticOrmus/LibreMobileDev-Grok-Build) · [SecOps](https://github.com/HermeticOrmus/LibreSecOps-Grok-Build) · [SessionFlow](https://github.com/HermeticOrmus/LibreSessionFlow-Grok-Build) · [WhatsApp](https://github.com/HermeticOrmus/LibreWhatsApp-Grok-Build)
- Skills collections: [grok-skills](https://github.com/HermeticOrmus/grok-skills) · [grok-build-skills](https://github.com/HermeticOrmus/grok-build-skills)
- Claude proof (upstream, not this inventory): [LibreFinTech-Claude-Code](https://github.com/HermeticOrmus/LibreFinTech-Claude-Code)
- https://ormus.solutions
