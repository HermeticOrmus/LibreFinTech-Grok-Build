---
name: payment-flow-review
description: Authorize/capture/settle/refund flow review — states and idempotency. Use when reviewing money-movement design you own. Documentation and design review only.
---

# Payment Flow Review

Review the state machine that moves money: authorize → capture → settle → refund (plus void, fail, and timeout). Truth over flattery. Measurable findings beat adjectives.

Gold Hat: name the money job first, then teach the failure mode while you flag it. A review that only lists defects extracts attention; a review that leaves a reusable rule empowers the next pass.

This skill is **documentation and design review only** — not legal advice, not a provider SDK, not a fraud recipe.

## When to use

- Designing or reviewing a payment integration you own or are authorized to review
- A report of double-charge, stuck authorized, or refund that does not match capture
- Pre-launch check of states, idempotency, and support-visible status

Do not use this skill to invent attack recipes, evasion steps, or exploit payloads. Hand KYC/AML policy to `kyc-aml-checklist` (stub). Hand ledger postings to `ledger-design` (melted). Hand who/what/when logs to `audit-trail` (melted). Call stubs; do not invent their depth.

## Hard rules

- Documentation and design review only — not legal advice.
- No fraud, evasion, or exploit guidance.
- Never embed real PANs, secrets, or customer PII in examples. Use toy amounts and fake IDs (`pi_toy_1`, `cust_toy_1`, `1000` minor units).

## Operating steps

1. **Name the money job.** Who pays, who receives, which rail, which currency, what success looks like. If unknown, ask. Guessing a capture amount is extraction.
2. **Draw the states you actually persist.** Happy path plus fail, void, timeout, partial capture, partial refund. If a state exists only in a provider dashboard, say so.
3. **Walk the checks below.** For each finding: location (endpoint, webhook, table), current behavior, why it fails, exact design fix.
4. **Rank by severity.** Critical → high → medium → low. Cap the first patch list at what a person can do in one sitting.
5. **Hand leftovers** to `ledger-design`, `audit-trail`, `reconciliation` (stub), or `financial-security-defaults` (stub) instead of writing a fake full audit.

Stop if you cannot name the money job. Ask.

## Checks (measurable)

### States

The system of record must know which money events have happened. Provider status is a source, not a substitute.

| Check | Pass | Fail |
|-------|------|------|
| Happy path | Authorize, capture, settle, and refund are named states with allowed transitions | Only `paid` / `unpaid` |
| Terminal vs pending | Fail, void, and expire are distinct from success | Timeout looks like success to support |
| Partial | Partial capture and partial refund have remaining-amount math in minor units | Full-only model silently drops leftovers |
| Out of order | Late capture or refund can land without inventing a prior state | Webhook timestamp trusted as sequence |

### Idempotency

Retries must not create a second money movement.

| Check | Pass | Fail |
|-------|------|------|
| Key on write | Client or server supplies a key; the same key + same intent returns the same result | Retry without a stored key |
| Scope | Key is bound to actor + intent + amount + currency | Key reused for a different amount |
| When checked | Dedup happens before the provider call and before the ledger write | Check after the side effect |
| Webhook | Provider event ID is stored; replay is a no-op | Dedupe by event type only |

### Timeouts and retries

| Check | Pass | Fail |
|-------|------|------|
| Auth window | Uncaptured auth has an expiry and a void/expire path | Auth sits forever as "pending" |
| Retry class | 5xx / timeout may retry with the same key; 4xx does not mint a new charge | Blind retry on every error |
| At-least-once | Webhook 2xx only after persistence commits | 200 returned, then write |

### Observable status

Support and the customer must see the same state the ledger believes.

| Check | Pass | Fail |
|-------|------|------|
| Support view | Status, last event id, remaining capturable, remaining refundable | Dashboard-only truth |
| Customer copy | Pending / succeeded / failed / refunded in plain language | Raw provider enum dumped |
| Amounts | Integer minor units + ISO currency; no float | `$10.1` from float math |

### PCI and secrets (design, not a full audit)

| Check | Pass | Fail |
|-------|------|------|
| Card data | Server sees tokens or a hosted field, never raw PAN/CVV | PAN in logs, examples, or your DB |
| Secrets | Webhook signing secret named as a secret; never printed | Secret in the review output |

A PCI or SOC mapping is `regulatory-map` (stub) plus counsel. Do not invent a certification score.

## Severity

| Rank | Meaning | Example |
|------|---------|---------|
| Critical | Can move money twice, lose money, or persist PAN | Retry without idempotency; raw PAN in logs |
| High | Stuck funds or support cannot tell state | Auth never expires; webhook order trusted |
| Medium | Edge math or observability debt | Partial refund remaining amount unverified |
| Low | Naming / docs | Provider enum shown to customers |

If unsure between two ranks, pick the higher and say why.

## Worked example — toy authorize then capture

Job: merchant captures `1000` minor units USD after a separate authorize. Toy IDs only.

Weak design (review input):

```text
POST /pay { amount: 10.00, customerId: "cust_toy_1" }
  → provider.charge()
  → UPDATE payments SET status='paid'
```

No idempotency key. Float amount. Single `paid` status. Capture and authorize collapsed. No webhook event id.

Critique (abridged):

```markdown
## Job
Merchant captures 1000 USD minor units after authorize. Primary action: capture.

## Findings
1. **Critical — idempotency.** POST /pay has no stored key; a client retry can charge twice.
   Remediation: require `Idempotency-Key`; persist key + result before the provider call; replay returns the first result.
2. **Critical — amounts.** `10.00` float. Remediation: `amount_minor: 1000`, `currency: USD`.
3. **High — states.** `paid` hides authorize vs capture vs settle. Remediation: persist `authorized` / `captured` / `settled` / `failed` with allowed transitions.
4. **High — webhooks.** No event-id dedupe. Remediation: store provider event id; replay is a no-op.

## Fixes now
1. Idempotency key on authorize and on capture.
2. Integer minor units.
3. Named states + remaining capturable.

## Leftovers
Postings → `ledger-design`. Who changed status → `audit-trail`. Daily expected-vs-actual → `reconciliation` (stub).
```

That is a review: locations, severity, remediations, leftovers. Not a `/10` scorecard, not a charge recipe.

## Output shape

```markdown
## Job
[who pays / who receives / rail / currency / success]

## States found
[authorized | captured | settled | refunded | voided | failed | …] — [persisted where?]

## Findings (severity-ranked)
1. **[Critical|High|Medium|Low] — [dimension].** [where] [what] [why]
   Remediation: [exact design change]
2. …

## Fixes now
1. …
2. …
3. …

## Leftovers
- [skill] — [what you did not pretend to finish]

## Residual risks
[unknowns; mark unverified if you did not see the code]
```

If nothing is wrong, say so. Empty findings are allowed. Invented issues are not.

## Quality bar

A pass is done when every finding is specific, ranked, and remediable, and the teach-while-fixing sentence is implicit in the *why*. Refuse "add fraud checks" without a defensive owner — that is `fraud-signals` (stub), still not a recipe.

## Suite

Doctrine: [grok-build-reality-os](https://github.com/HermeticOrmus/grok-build-reality-os). Gold Hat: [GOLD_HAT.md](https://github.com/HermeticOrmus/LibreFinTech-Grok-Build/blob/main/GOLD_HAT.md). Sibling Libre*-Grok-Build packs: [README suite footer](https://github.com/HermeticOrmus/LibreFinTech-Grok-Build/blob/main/README.md).
