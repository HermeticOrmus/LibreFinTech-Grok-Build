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

Dogfood copies of every skill live at `.grok/skills/<name>/SKILL.md` and must match `skills/<name>/SKILL.md`.

Quality ladder (hygiene, not a badge): this pass targets [L3–L4](https://github.com/HermeticOrmus/grok-build-reality-os/blob/main/docs/QUALITY_LADDER.md). It does not claim L5.

## Suite

Doctrine: [grok-build-reality-os](https://github.com/HermeticOrmus/grok-build-reality-os). Sibling Libre*-Grok-Build packs: [README suite footer](../README.md).
