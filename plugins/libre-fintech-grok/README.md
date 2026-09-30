# libre-fintech-grok

The Grok-native layer of [LibreFinTech-Grok-Build](https://github.com/HermeticOrmus/LibreFinTech-Grok-Build): three skills melted for Grok Build.

| Skill | Job |
|-------|-----|
| `payment-flow-review` | Authorize/capture/settle/refund: states and idempotency |
| `ledger-design` | Double-entry sketch: accounts, postings, immutability |
| `audit-trail` | Who/what/when without leaking secrets or PII |

## Install

```bash
grok plugin marketplace add HermeticOrmus/LibreFinTech-Grok-Build
grok plugin install libre-fintech-grok@libre-fintech-grok
```

The same marketplace offers every LibreFinTech-Claude-Code plugin, pinned by commit.

The stubs (`kyc-aml-checklist`, `reconciliation`, `regulatory-map`, `fraud-signals`, `financial-security-defaults`) and the stub orchestrator are not part of this plugin. They live in [`stubs/`](https://github.com/HermeticOrmus/LibreFinTech-Grok-Build/tree/main/stubs), and each names the pack plugin with the real depth. Honest table: [docs/DEPTH_MATRIX.md](https://github.com/HermeticOrmus/LibreFinTech-Grok-Build/blob/main/docs/DEPTH_MATRIX.md).

Gold Hat: [GOLD_HAT.md](https://github.com/HermeticOrmus/LibreFinTech-Grok-Build/blob/main/GOLD_HAT.md)
