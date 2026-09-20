# Quick Start — LibreFinTech for Grok Build

> From a clean machine to one payments/compliance review cue in under 5 minutes.

Doctrine first: put [grok-build-reality-os](https://github.com/HermeticOrmus/grok-build-reality-os) `AGENTS.md` on the machine (global Grok doctrine). This pack does not replace it.

## Prerequisites

- `git`
- Grok Build installed and able to see skills under `.grok/skills/` or `~/.grok/skills/`
- A payments or ledger system you **own** or are **authorized** to review, **or** this repo as the working tree

## Layout this file assumes

Verified against this repository (do not invent extra folders):

```
skills/<name>/SKILL.md            # canonical skill bodies (copy these)
AGENTS/fintech-orchestrator.md
docs/DEPTH_MATRIX.md
docs/MELT_RULES.md
.grok/skills/<name>/SKILL.md      # dogfood copy; must match skills/
.grok/plugins/librefintech-core/  # plugin stub; not required for first run
```

Melted (usable now): `skills/payment-flow-review/SKILL.md`, `skills/ledger-design/SKILL.md`, `skills/audit-trail/SKILL.md`.
Still stubs: the other five skills + the orchestrator. Honest table: [docs/DEPTH_MATRIX.md](./docs/DEPTH_MATRIX.md).

## Install (pick one)

### A. Dogfood this repo (fastest)

```bash
git clone https://github.com/HermeticOrmus/LibreFinTech-Grok-Build.git
cd LibreFinTech-Grok-Build
# Skills are already at .grok/skills/ — open this folder in Grok Build.
```

### B. Install into your payments project

```bash
git clone https://github.com/HermeticOrmus/LibreFinTech-Grok-Build.git ~/LibreFinTech-Grok-Build
cd /path/to/your-payments-project
mkdir -p .grok/skills
cp -R ~/LibreFinTech-Grok-Build/skills/* .grok/skills/
```

Confirm the copy landed:

```bash
test -f .grok/skills/payment-flow-review/SKILL.md
test -f .grok/skills/ledger-design/SKILL.md
test -f .grok/skills/audit-trail/SKILL.md
ls .grok/skills
```

You should see eight skill directories, matching `skills/` in this repo.

### C. User-global

```bash
git clone https://github.com/HermeticOrmus/LibreFinTech-Grok-Build.git ~/LibreFinTech-Grok-Build
mkdir -p ~/.grok/skills
cp -R ~/LibreFinTech-Grok-Build/skills/* ~/.grok/skills/
```

Same three `test -f` checks as B, under `~/.grok/skills/`.

Copy `AGENTS/fintech-orchestrator.md` only when you want a multi-skill pass. It is still a stub coordinator. Merge into existing project `AGENTS.md` / `.grok/AGENTS.md` — do not overwrite Reality OS doctrine.

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

- [ ] `payment-flow-review`, `ledger-design`, and `audit-trail` files exist at the install path you chose
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
