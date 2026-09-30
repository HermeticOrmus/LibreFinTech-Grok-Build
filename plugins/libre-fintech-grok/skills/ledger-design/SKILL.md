---
name: ledger-design
description: Double-entry ledger sketch — accounts, postings, immutability, and idempotent writes. Use when designing or reviewing a money system of record. Toy amounts only.
---

# Ledger Design

Sketch a double-entry system of record: chart of accounts, posting rules, immutability, and how balances are derived. The ledger catches what a processor dashboard misses.

Gold Hat: teach the invariant while you draw the accounts. A sketch that hides why debit equals credit extracts; a sketch that leaves the next engineer able to post a refund unaided empowers.

This skill is **documentation and design review only** — not a CPA product, not tax advice, not a fraud recipe.

## When to use

- Designing a new money movement system (do this before, or with, `payment-flow-review`)
- Migrating from "we look at the provider dashboard" to an owned ledger
- Debugging "balance does not match" as a *design* question (posting rules, not live recon)
- Adding a refund, payout, fee, or FX posting path

Do not use this skill as a general ledger for an accounting department, as an analytics warehouse, or as a log dump. Daily expected-vs-actual is `reconciliation` (still a stub) — call it; do not invent its depth. Who changed a posting rule is `audit-trail` (melted).

## Hard rules

- Documentation and design review only — not legal or accounting advice.
- No fraud, evasion, or exploit guidance.
- Never embed real PANs, secrets, or customer PII. Toy amounts and fake account names only (`1000` minor units, `acct_processor`, `acct_merchant_escrow`).
- Integer minor units. Never floats.

## Operating steps

1. **Name the money events.** What can happen: authorize, capture, fee, payout, refund, FX, correction. If an event cannot be posted, it is not in this ledger yet.
2. **Sketch the chart of accounts** with type (asset / liability / revenue / expense / equity) and currency. One account, one currency.
3. **Write posting rules** as debit/credit pairs (or balanced multi-legs) in minor units. Sum of debits = sum of credits *per currency*.
4. **State immutability.** Events and entries are append-only. Corrections are new compensating events that point at the original id.
5. **Name recon hooks.** Which external id (provider charge, bank transfer) lives on the event so `reconciliation` can match later.
6. **Propose toy fixtures** (fake amounts) that prove the invariant — not production data.

Stop if you cannot name at least one balanced posting. Ask.

## Checks (measurable)

### Double-entry invariant

| Check | Pass | Fail |
|-------|------|------|
| Legs | Every event has at least two entries | Single-sided "balance +=" |
| Balance | Per currency, sum(debits) = sum(credits) | Mixed USD+EUR in one total |
| Atomicity | Event + entries commit together | Entry written, event missing |
| Enforcement | Constraint, trigger, or equivalent — not "we remember" | Invariant only in a comment |

Account-type reminder (convention, not taste):

| Type | Debit means | Credit means |
|------|-------------|--------------|
| Asset | Increase | Decrease |
| Liability | Decrease | Increase |
| Revenue | Decrease | Increase |
| Expense | Increase | Decrease |
| Equity | Decrease | Increase |

### Chart of accounts

| Check | Pass | Fail |
|-------|------|------|
| Named job | Each account has a one-line purpose | `misc`, `temp`, `adjustments` as a junk drawer |
| Currency | Account is single-currency | Wallet row holding USD and EUR together |
| Ownership | Asset vs liability is explicit (who owes whom) | Merchant escrow typed as revenue |

### Immutability and corrections

| Check | Pass | Fail |
|-------|------|------|
| No mutate | No UPDATE/DELETE of posted events or entries | "Fix the row" runbook |
| Correction | New event with `corrects: <id>` and reversing legs | Silent overwrite |
| Trace | Correction reason + actor id (no PII dump) | Anonymous balance patch |

### Amounts and rounding

| Check | Pass | Fail |
|-------|------|------|
| Minor units | Integer cents / yen / etc. | Float `10.1` |
| Split remainder | Extra minor unit has an owner or a rounding account | Three-way split that does not sum |
| FX | Rate snapshotted on the event; each currency balances alone | `$100 + €92` as one number |

### Derived balances

Balances are views (or maintained projections) of events — not a second source of truth you edit by hand.

| Check | Pass | Fail |
|-------|------|------|
| Derivation | Balance can be rebuilt from events | Balance column edited in prod |
| Staleness | Refresh policy named (on-write, cron, eventual) | Unstated |
| Recon hook | External id on the event | Nothing to match at EOD |

## Severity

| Rank | Meaning | Example |
|------|---------|---------|
| Critical | Invariant can break or history can be rewritten | UPDATE on entries; float money |
| High | Money job cannot be posted correctly | Refund has no reversing pair |
| Medium | Recon or FX debt | Missing provider id; no rounding account |
| Low | Naming | Account label unclear but type is right |

## Worked example — toy $10 capture with a $0.50 fee

Job: processor captures `1000` USD minor units; platform fee `50`; merchant escrow `950`. Toy accounts only.

Weak design:

```text
UPDATE merchants SET balance = balance + 10.00 WHERE id = 'm_toy';
```

Single-sided, float, mutable balance, no event, no fee leg.

Stronger sketch (principle-tagged):

```text
EVENT capture_toy_1
  currency: USD
  amount_minor: 1000
  external_id: ch_toy_1
  accounts:
    DEBIT  acct_processor_asset     1000   # asset up (cash at processor)
    CREDIT acct_merchant_escrow      950   # liability up (we owe merchant)
    CREDIT acct_platform_fee_rev      50   # revenue up
```

- **Invariant:** 1000 = 950 + 50. One currency.
- **Types:** processor asset; escrow liability; fee revenue.
- **Immutability:** this event is never updated. A wrong fee becomes a correction event that reverses and reposts.
- **Recon hook:** `ch_toy_1` for later expected-vs-actual.

Three concrete fixes if you only have the weak UPDATE: (1) append an event + two-or-more legs, (2) integer minor units, (3) stop writing `merchants.balance` by hand — derive it.

Payout later (same toy):

```text
EVENT payout_toy_1
  DEBIT  acct_merchant_escrow   950
  CREDIT acct_bank_asset        950
```

Refund later must reverse the capture legs (and name who approved it in `audit-trail`, not in this posting).

## Output shape

```markdown
## Job
[events this ledger must record]

## Chart
| Account | Type | Currency | Purpose |
|---------|------|----------|---------|

## Posting rules
[event → debit/credit legs in minor units]

## Invariant
[how debit=credit is enforced]

## Immutability
[correction event shape]

## Recon hooks
[external ids]

## Toy fixtures
[one balanced example; fake amounts]

## Findings
- [severity] — [what] → [needed]

## Leftovers
- [skill] — [not pretended]
```

If the existing design already balances, say so. Do not invent accounts the product does not need.

## Quality bar

A pass is done when a second engineer can post the next refund from the sketch without asking where the other leg goes. Refuse dashboard-only "ledgers." Refuse real customer amounts in the write-up.

## Suite

Doctrine: [grok-build-reality-os](https://github.com/HermeticOrmus/grok-build-reality-os). Gold Hat: [GOLD_HAT.md](https://github.com/HermeticOrmus/LibreFinTech-Grok-Build/blob/main/GOLD_HAT.md). Sibling Libre*-Grok-Build packs: [README suite footer](https://github.com/HermeticOrmus/LibreFinTech-Grok-Build/blob/main/README.md).
