# Treasure View — Brief (future stage)

## Why

Right now the Treasure (the person actually doing the job) only finds out
what's been quoted and what they'll be paid second-hand — a call, a text, a
figure written on a job sheet. The brief below is a spec for a lightweight,
Treasure-facing view of the same quote data so they can check it themselves,
without giving them visibility into customer pricing or your margin.

Not built yet — this is a plan to implement once the customer-facing side is
solid.

## Who sees it, and what

Two audiences, two very different slices of the same `quote` object:

| Field | Customer view | Treasure view |
|---|---|---|
| Job description / project comments | ✅ | ✅ |
| Site photos | ✅ | ✅ |
| Customer name, address, mobile | ✅ (their own) | ✅ (needed to do the job) |
| Line items (description, qty) | ✅ | ✅ |
| Customer price (what they're charged) | ✅ | ❌ |
| **Treasure payout** (`internal.labour`) | ❌ | ✅ |
| Materials list (item/cost/supplier) | ❌ | ✅ (they may be sourcing them) |
| Deposit, discount, terms | ✅ | ❌ |
| Fee %, profit, margin, markup | ❌ | ❌ (business-only, stays internal) |
| Internal notes | ❌ | ❌ (unless a note is explicitly flagged "share with Treasure") |

The Treasure should never see the customer price or your fee/margin — only
what the job involves and what they personally get paid for it. That keeps
the current "Internal Margins & Notes" tab exactly as private as it is today;
the Treasure view is a *third*, separate lens on the data, not a relaxed
version of the internal tab.

## Proposed shape

- A **Treasure Brief** — one page per quote, generated the same way the
  customer quote is (from the same `quote` object), showing: job description,
  photos, address/contact, line items (descriptions only, no prices), the
  materials list, and a single clear "You'll be paid: £X" figure sourced from
  `internal.labour`.
- An optional **"share with Treasure" flag** on internal notes, so specific
  notes (e.g. "customer has a dog", "park round back, no driveway access")
  can cross over without exposing the whole internal tab.
- Delivery: same pattern as the customer send — a link or PDF, sent once a
  Treasure is assigned to the job, not before (so it isn't sent to someone
  who won't end up doing the work).

## Open questions to settle before building

1. **Multiple Treasures per job** — does payout ever get split, and if so how
   should that be entered (today `internal.labour` is a single figure)?
2. **When does it get generated** — automatically once you mark a Treasure as
   assigned, or a manual "Send to Treasure" button like the customer one?
3. **Does the Treasure need to accept/confirm** the job through this view, or
   is it read-only reference?
4. **Hosting** — this depends on the same infrastructure decision as
   emailing the customer quote (see main README): a fully static app can
   still produce a Treasure PDF/print view, but a real shareable link needs
   a backend to persist and serve it.
