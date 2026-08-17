# Treasure View

## What's built (Treasure Brief tab)

The app now has a third tab, 🧰 **Treasure Brief**, separate from the
customer-facing quote and the internal margin calculator:

- **Job details** — customer name, address, mobile, and the job description,
  read live from the Customer Quote tab (no need to re-type it).
- **Site/reference photos** — these live here now, not on the customer quote
  or its PDF. Photos are for whoever's doing the work, not the customer.
- **Their Estimate** — an intake form for the Treasure to fill in on site:
  hours or days needed, a rate, and a materials-needed list (item/qty/notes).
- **Download Treasure Brief PDF** — job description, photos, and the
  estimate fields (blank ruled lines if not filled in yet, for a paper
  hand-off) — no customer pricing anywhere on it.
- **Send My Estimate to Office** — same one-tap share/PDF pattern as the
  customer send, but addressed to your own business email (from Settings)
  instead of the customer's, carrying the Treasure's hours/days and
  materials list back to you.
- **Apply Estimate to Internal Margins** — one click copies hours×rate into
  `internal.labour` and the materials list into `internal.materialsList`, so
  once a number comes back from the Treasure you can immediately see the
  margin on the Internal tab.

This covers the workflow: assess the job → hand the brief to a Treasure →
they estimate time and materials → it comes back to you → you price the job.

## What's still open (a later stage)

The original idea for this tab was a **payout view** — once a job is priced
and a Treasure is confirmed, showing them what they'll be paid
(`internal.labour`) without exposing the customer price or your margin. That's
a different moment in the workflow from the intake form above (post-pricing
vs. pre-pricing) and isn't built yet. Worth revisiting once the estimate
intake has been used for real and it's clear whether a separate payout
confirmation is still needed, or whether a phone call covers it fine.

Open questions if it gets built:

1. **Multiple Treasures per job** — does payout ever get split, and if so how
   should that be entered (today `internal.labour` is a single figure)?
2. **Confirmation** — read-only reference, or does the Treasure need to
   accept/confirm the job through it?
3. **Hosting** — a fully static app can still produce a payout PDF, but a
   real shareable link (rather than a manually-passed file) needs a backend
   to persist and serve it — same trade-off as emailing the customer quote,
   see the main README.
