---
name: audit-trail
description: Who/what/when audit trail without leaking secrets or PII. Use when reviewing money, access, or compliance-relevant actions. Design review only.
---

# Audit Trail

Design a who / what / when record for money and privileged actions — without turning the log into a second copy of secrets or customer PII.

Gold Hat: teach *why* a field is in or out. A trail that dumps PANs "for completeness" extracts. A trail that a support engineer can query, and a customer can trust will not republish their card, empowers.

This skill is **documentation and design review only** — not legal advice, not a surveillance product, not a fraud recipe.

## When to use

- Reviewing whether money-state changes are attributable
- Adding privileged actions (refunds, limit changes, KYC decision recorded as *that a decision happened*)
- Preparing a support or compliance query path
- Finding PII or secrets already leaking into logs

Do not use this skill to design covert monitoring of people, to evade audit, or to reconstruct cardholder data. Ledger *amounts and accounts* are `ledger-design` (melted). Payment *states* are `payment-flow-review` (melted). KYC document checklists are `kyc-aml-checklist` (stub) — call the stub; do not invent a full AML program.

## Hard rules

- Documentation and design review only — not legal advice.
- No fraud, evasion, or exploit guidance.
- Never embed real PANs, secrets, government IDs, or customer PII in examples or in recommended log payloads. Use fake actor ids (`actor_ops_1`) and fake object ids (`pay_toy_1`).
- Prefer tokens and last-4 *only if the product already stores them lawfully*; do not add raw PAN "for audit."

## Operating steps

1. **Name the events worth auditing.** Money-state changes, permission changes, export of customer data, override of a control. If everything is audited, nothing is queryable — pick the money-relevant set first.
2. **Require actor + object + time + action.** Actor is a durable id (user, service, or `unknown` if truly system). Object is the payment, account, or policy — not a dump of its fields.
3. **Write redaction rules** before retention. What must never appear: PAN, CVV, full ID document, password, webhook secret, session token.
4. **State retention and mutability.** Append-only. Corrections are new rows that point at the original. Retention is a named policy, not "forever unless disk fills."
5. **Name the query path.** Who may read the trail, for what job (support, compliance), and how they avoid pulling PII columns that should not exist.

Stop if the proposed payload includes a secret or a raw identifier. Cut it. That is the review.

## Checks (measurable)

### Who / what / when

| Check | Pass | Fail |
|-------|------|------|
| Actor | Durable id + actor type (human / service) | Shared `admin` login with no person |
| Action | Verb from a small enum (`refund_requested`, `limit_changed`) | Free-text "updated stuff" |
| Object | Type + id | Whole customer row serialized |
| Time | UTC timestamp the writer controlled | Client-supplied time as truth |
| Correlation | Request or money-event id links related rows | Orphan status change |

### Redaction

| Check | Pass | Fail |
|-------|------|------|
| Secrets | Signing secrets, passwords, tokens absent | Webhook secret in `after_state` |
| Card data | No PAN/CVV; token or (if already lawful) last-4 only | Full card in the audit table |
| PII budget | Name/email only if required for the query job; else actor/object ids | KYC image bytes in the log |
| Before/after | Field-level diffs of *non-sensitive* policy or amount | Full record snapshot "just in case" |

### Mutability and integrity

| Check | Pass | Fail |
|-------|------|------|
| Append-only | Application role cannot UPDATE/DELETE audit rows | "Fix the log" UPDATE |
| Correction | New row `corrects: <id>` + reason + actor | Silent edit |
| Integrity | Tamper-evident design named (hash chain, WORM, or equivalent) *or* marked **unverified** | "Immutable" with no mechanism |
| Separation | Audit store is not the same writable pool as the app DB *or* the risk is named | One SQL injection loses both |

Do not claim cryptographic integrity you did not verify.

### Retention and access

| Check | Pass | Fail |
|-------|------|------|
| Retention | Duration + legal owner named (and "not legal advice") | Infinite, unowned |
| Read path | Role + purpose (support ticket, compliance export) | Every engineer `SELECT *` |
| Export | Export itself is an audited event | Silent dump to a laptop |

### Query for support / compliance

| Check | Pass | Fail |
|-------|------|------|
| By money object | "Show events for `pay_toy_1`" works | Only full-table scan stories |
| By actor | "What did `actor_ops_1` change today?" works | No actor index |
| Absence | Missing event is visible as a gap (or said unverified) | "If it is not logged it did not happen" without evidence |

## Severity

| Rank | Meaning | Example |
|------|---------|---------|
| Critical | Secrets or PAN can land in the trail, or money moves with no actor | Webhook secret logged; refund with no actor |
| High | Trail can be rewritten or is unqueryable for the job | UPDATE on audit rows; no object id |
| Medium | Retention or access debt | Infinite retain; shared read role |
| Low | Naming | Verbose action strings, enum still closed |

## Worked example — toy refund approval

Job: ops approves a `1000` minor-unit USD refund on `pay_toy_1`. No real customer.

Weak design:

```text
LOG "admin refunded card 4242... and secret=whsec_live"
UPDATE audit SET action='ok' WHERE id=9;
```

PAN-like data, secret, mutable row, no structured actor/object.

Stronger event (fields only — not a logging product):

```text
AUDIT refund_approved
  at: 2026-09-20T00:00:00Z
  actor_id: actor_ops_1
  actor_type: human
  action: refund_approved
  object_type: payment
  object_id: pay_toy_1
  amount_minor: 1000
  currency: USD
  correlation_id: evt_toy_1
  # no PAN, no secret, no email body
```

If the amount was wrong, **do not update**. Append:

```text
AUDIT audit_correction
  corrects: <prior_audit_id>
  reason: amount_minor misstated (ops error)
  actor_id: actor_ops_2
```

Three concrete fixes from the weak log: (1) structured actor/action/object, (2) drop PAN and secrets from the payload, (3) append-only + correction row. Then run `ledger-design` for the posting pair and `payment-flow-review` for remaining refundable.

## Output shape

```markdown
## Job
[which actions must be attributable]

## Event list
[action enum + object types]

## Record shape
[actor, action, object, time, correlation — and what is forbidden]

## Redaction
[never-log list]

## Retention + access
[duration, owner, read path]

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
```

If the trail is already clean, say so. Do not invent events the product cannot emit.

## Quality bar

A pass is done when a support engineer can answer "who refunded `pay_toy_1` and when" without seeing a secret, and a second engineer knows how to correct a wrong row without UPDATE. Refuse vibe-only "add more logging."

## Suite

Doctrine: [grok-build-reality-os](https://github.com/HermeticOrmus/grok-build-reality-os). Gold Hat: [GOLD_HAT.md](https://github.com/HermeticOrmus/LibreFinTech-Grok-Build/blob/main/GOLD_HAT.md). Sibling Libre*-Grok-Build packs: [README suite footer](https://github.com/HermeticOrmus/LibreFinTech-Grok-Build/blob/main/README.md).
