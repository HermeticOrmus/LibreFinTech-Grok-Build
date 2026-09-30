# Depth matrix

Update this table when melting. Status words mean what they say:

| Status | Meaning |
|--------|---------|
| stub | Thin cue only. Usable as a reminder, not a playbook. |
| melted | Real Grok skill: when-to-use, steps, measurable checks, example, output shape. |

Never copy Claude plugin / agent / command totals into this inventory. Upstream [LibreFinTech-Claude-Code](https://github.com/HermeticOrmus/LibreFinTech-Claude-Code) is proof that the *job* exists, not a count this repo has earned.

| ID | Kind | Status | Source (Claude, for melt) | Notes |
|----|------|--------|---------------------------|-------|
| payment-flow-review | skill | melted | plugins/payment-processing | States, idempotency, toy example. Design review only. |
| ledger-design | skill | melted | plugins/ledger-design | Double-entry, immutability, recon hooks. Toy amounts. |
| audit-trail | skill | melted | plugins/audit-trails | Who/what/when + redaction. No PII/secret payloads. |
| kyc-aml-checklist | skill | stub | plugins/kyc-aml | Policy framing cue only. Not evasion. |
| reconciliation | skill | stub | plugins/reconciliation | Daily recon cue only. |
| regulatory-map | skill | stub | plugins/regulatory-compliance | Theme map cue only. Not a legal opinion. |
| fraud-signals | skill | stub | plugins/fraud-detection | Defensive cue only. No attack recipes. |
| financial-security-defaults | skill | stub | plugins/financial-security | Auth/secrets cue only. |
| fintech-orchestrator | agent | stub | LibreFinTech-Claude-Code agents | Coordinates the skills; not a melted specialist. |

This repo now: **3 melted skills**, **5 stub skills**, **1 stub agent**.

Dogfood copies of every skill live at `.grok/skills/<name>/SKILL.md` and must match their source: `plugins/libre-fintech-grok/skills/<name>/SKILL.md` for melted skills, `stubs/skills/<name>/SKILL.md` for stubs. CI checks it.

## v1.0.0: where each row lives

Melted skills install as the `libre-fintech-grok` plugin. Stubs stay in `stubs/` and never install; each names the pack plugin that holds the real depth. The 21 pack plugins install from the same marketplace, pinned to one commit of [LibreFinTech-Claude-Code](https://github.com/HermeticOrmus/LibreFinTech-Claude-Code) (see `.grok-plugin/marketplace.json`). They are installed depth, not this repo's inventory.

| ID | Lives at | Installs | Real depth, installed by this marketplace |
|----|----------|----------|-------------------------------------------|
| payment-flow-review | `plugins/libre-fintech-grok/skills/payment-flow-review/` | yes, in `libre-fintech-grok` | this skill |
| ledger-design | `plugins/libre-fintech-grok/skills/ledger-design/` | yes, in `libre-fintech-grok` | this skill |
| audit-trail | `plugins/libre-fintech-grok/skills/audit-trail/` | yes, in `libre-fintech-grok` | this skill |
| kyc-aml-checklist | `stubs/skills/kyc-aml-checklist/` | no | `kyc-aml` |
| reconciliation | `stubs/skills/reconciliation/` | no | `reconciliation` |
| regulatory-map | `stubs/skills/regulatory-map/` | no | `regulatory-compliance` |
| fraud-signals | `stubs/skills/fraud-signals/` | no | `fraud-detection` |
| financial-security-defaults | `stubs/skills/financial-security-defaults/` | no | `financial-security` |
| fintech-orchestrator | `stubs/agents/fintech-orchestrator.md` | no | a specialist agent in each pack plugin |

Quality ladder (hygiene, not a badge): this pass targets [L3–L4](https://github.com/HermeticOrmus/grok-build-reality-os/blob/main/docs/QUALITY_LADDER.md). It does not claim L5.

## Suite

Doctrine: [grok-build-reality-os](https://github.com/HermeticOrmus/grok-build-reality-os). Sibling Libre*-Grok-Build packs: [README suite footer](../README.md).
