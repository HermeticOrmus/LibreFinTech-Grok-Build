# Quick Start — LibreFinTech for Grok Build

> From zero to a payments/compliance review cue in under 5 minutes.

## Prerequisites

- Grok Build installed and working
- A payments or ledger system you own / are authorized to review

## Install skills (repo-local)

```bash
git clone https://github.com/HermeticOrmus/LibreFinTech-Grok-Build.git
cd your-project
mkdir -p .grok/skills
cp -R /path/to/LibreFinTech-Grok-Build/skills/* .grok/skills/
```

Or user-global:

```bash
mkdir -p ~/.grok/skills
cp -R /path/to/LibreFinTech-Grok-Build/skills/* ~/.grok/skills/
```

## First-run teach cue

1. **Flow** — "Run payment-flow-review on authorize → capture → settle → refund."
2. **Ledger** — "Run ledger-design for double-entry and idempotency."
3. **Audit** — "Run audit-trail for who/what/when without PII leakage."

## Hard rules

- Documentation and design review only — not legal advice.
- No fraud, evasion, or exploit guidance.
- Never embed real PANs, secrets, or customer PII in examples.

## Smoke checklist

- [ ] Skills visible to Grok
- [ ] One skill run produces measurable output
- [ ] No secrets in output
