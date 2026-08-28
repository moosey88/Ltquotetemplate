# Quote & Estimate Builder

A single-file, no-build web app for putting together a customer quote/estimate
on the spot — fill in customer details, add line items and site photos, and
print/email it in a couple of minutes. Modeled on the Local Treasures
"ESTIMATE TEMPLATE" format (customer quote + a separate internal margin sheet).

## Using it

Just open `index.html` in a browser — no server or build step needed. To make
it available on your phone in the field, host it as a static site (e.g.
GitHub Pages: Settings → Pages → deploy from the `main` branch / root).

### Customer Quote tab
- Date, reference #, valid-until, prepared-by, and customer details
- Project comments (prefilled from your default terms/description in Settings)
- Line items table (description, qty, unit price) with an auto-calculated total.
  Each item has an optional "+ Add details" field for a longer description —
  useful context for bigger jobs, skippable for something as simple as
  putting up a blind. A built-in library of starter snippets for common job
  types (handyman, gardening, decorating, plumbing, etc.) gives a starting
  point to edit rather than a blank box.
- Discount — quick 5/10/15% buttons, or a custom % or £ amount with a reason,
  applied to the subtotal before deposit/total
- Deposit % and total, calculated live
- **"+ Add from Job Bank"** — pulls a line item straight from the Job Bank
  (see below) instead of typing it from scratch, and tags it so a later
  Won/Lost outcome feeds back into that job's pricing history
- **Outcome** (Pending / Won / Lost) — set once you know how the quote went.
  Won or Lost updates the price history of any items that came from the Job
  Bank; Lost also offers to drop their price 10% for next time
- Terms & conditions text
- Footer with your contact and bank details (from Settings)

No site photos here — they're deliberately left off the customer-facing
quote and PDF, and live on the Treasure Brief tab instead.

### 📚 Job Bank tab
A running library of "what should this job cost" answers, so you only have
to work it out once per job type, shown as a table you can scan and act on
fast:
- **+ New Job Request** — adds a row and opens it for editing. Fill in the
  job name, and hit **🔎 Research going rate** to open a search (pre-filled
  with the job name and your Service Area from Settings) across
  Checkatrade, MyBuilder, and MyJobQuote in one tab — skim the results and
  type what you find into Price Range / Current Price / Research Notes.
  This stays a one-click search rather than an automatic scan because a
  fully static app has nowhere safe to keep an API key — see "Data &
  privacy" below. You can still ask Claude in chat for a deeper look (it
  also checks your own pricing history in Drive first) and paste that in
  instead
- **🌱 Load 50 Common Jobs** — one click adds 50 of the most common
  requests (handyman, electrics, plumbing, gardening, cleaning,
  decorating), each with a Price Range pulled from your own quoting sheet,
  regular-requests log, and GBP profile pricing — already there, so you're
  not starting from a blank table. Fill in Current Price and Time Taken
  yourself for each; safe to click again later, it skips anything already
  in the bank by name
- The table shows, per job: **Price Low–High** (the going-rate benchmark),
  with the Current Price underneath — the one you'll actually quote — and,
  once you've entered one, a badge showing whether it's **below**, **at**,
  or **above** that range. **Time Low–High** (hours the job typically
  takes), **Materials** (a typical estimated cost), and **Treasure Cost
  Low–High** — an internal-only pay budget, separate from the customer
  price, so you can see at a glance how much room there is to pay a slower
  Treasure more without the customer's price changing. None of this —
  including the Treasure Cost budget — is ever sent to a Treasure; see the
  Treasure Link section below for why that's structural, not just hidden
- **+ Use** on a row adds it straight to the current quote at the Current
  Price, and — only where those fields are still blank, so a real Treasure
  estimate never gets overwritten — seeds the Treasure's hours (midpoint of
  the time range), a materials line at the estimated cost, and an Internal
  note stating the pay budget range, then jumps you to the Customer Quote
  tab. This is the fast path: research once, then add to quote in one click
  from then on
- Click the ▸ next to a job name to expand it for editing — category,
  status, price/time/materials/budget fields, research notes, and (once
  it's been quoted) **Log Win** / **Log Loss**. **Status**: Researching
  (still working out the number) or Active (ready to use on quotes) — the
  "+ Add from Job Bank" picker on the Customer Quote tab only offers Active
  jobs. **Log Loss** prompts for a new, lower price to try next time
  (pre-filled with a 10% cut, edit to whatever you want) — the same result
  also happens automatically if you mark a quote's Outcome as Lost when it
  used this job
- A short history per job (win/loss record and the last few price points)
  so you can see how a job's price has moved over time

### 🧰 Treasure Brief tab
For whoever's actually doing the job — a separate document from the
customer quote, with no pricing on it:
- Job details (customer name, address, mobile, job description) — read live
  from the Customer Quote tab, nothing to re-type
- Site/reference photos with captions
- An estimate intake form for the Treasure to fill in: hours or days needed
  (no rate — pay is worked out individually, not by formula) and a
  materials-needed list with item / qty / estimated cost / notes, plus a
  reminder that materials are bought by the Treasure and reimbursed against
  receipts
- **Download Treasure Brief PDF** — job info + photos + estimate fields
  (blank ruled lines if not filled in, so it works as a paper hand-off too)
- **Send My Estimate to Office** — same one-tap share/PDF flow as the
  customer send, but addressed to your own business email instead, carrying
  the Treasure's time and materials estimate back to you
- **Apply Estimate to Internal Margins** — copies the hours/days estimate
  into the Internal tab's notes as a reference for setting pay, and copies
  the materials list (with their estimated costs) across, summed straight
  into the Materials Cost field
- **Get Link for Treasure** — generates a URL a Treasure can open on their
  own phone to fill in the estimate themselves, without ever seeing the
  customer quote. The link carries only job details (reference, date,
  customer name/address/mobile, job description) — never line items,
  discount, deposit, terms, or the internal margin fields, so there's
  nothing for their device to receive in the first place, not just
  something hidden by CSS. Opening it drops into a stripped-down
  single-page view: no tabs, no admin controls, just Job Details, Photos,
  and Their Estimate. When they hit "Send My Estimate to Office," the
  message includes a reply link — opening that back on the device that has
  the matching quote saved (matched by reference) imports their estimate
  straight into it and jumps to the Treasure tab, no re-typing. If that
  quote isn't on the device that opens the reply link, it shows the
  received data in an alert instead of silently failing.

### Internal Margins & Notes tab
Never printed and not included when you email the quote. Use it to work out
whether the price actually makes sense:
- Revenue is pulled automatically from the quote total
- Enter your fee % (franchise/platform/referral cut), labour cost, and
  materials cost
- A materials list (item / cost / supplier / notes) that can be summed
  straight into the materials cost field
- Auto-calculated profit before fee, fee amount, net profit, net margin %,
  and markup %
- A free-text notes box for anything else worth remembering about the job

## Settings

Click **Settings** to set your company name, logo, contact details, bank
details, a link to your full Terms & Conditions, a Service Area (used to
localise the Job Bank's "Research going rate" search links, e.g. "Farnham,
Surrey"), and the defaults that get pre-filled on every new quote (deposit
%, fee %, quote validity in days, default terms, default project comments).

Defaults are pre-filled to match the Local Treasures template: the logo
(`assets/logo.png`), phone (0333 577 1188), website, bank account and sort
code, and the T&Cs link. `preparedBy` and `email` are deliberately left
blank — those are personal to whoever's sending the quote, so fill in your
own rather than a shared default.

Uploading your own logo redraws it through a canvas before storing it, which
strips EXIF/XMP metadata (common in phone photos) that otherwise makes the
PDF library reject the image, and scales it down to keep generated PDFs a
sane size — the logo shows correctly on screen and in Print either way, but
without this step it would silently fail to appear in the exported PDF.

## Saving & sending

- **Save** stores the current quote in the browser (localStorage) so you can
  come back to it later via the **Load saved quote** dropdown. Save only
  stores locally — it doesn't touch Drive, since it fires on every draft
  edit and would otherwise flood Drive with half-finished copies. Download
  PDF and Send are what actually back a quote up (see below).
- **Print** opens the browser print dialog with the internal tab and all app
  chrome hidden — "Save as PDF" from there gives you a clean customer-facing
  document too.
- **Download PDF** generates a properly formatted quote PDF (header, customer
  details, photos, line items, discount, totals, terms, footer) using the
  vendored `jspdf` library — works fully offline, no server involved.
- **Send to Customer** builds the same PDF and hands it to your device's
  native share sheet (`navigator.share`) so on a phone you can tap through to
  Mail/Messages/WhatsApp with the PDF already attached — genuinely one tap on
  supported mobile browsers. On desktop browsers that don't support sharing
  files, it falls back to downloading the PDF and opening a pre-filled email
  (recipient, subject, plain-text summary) for you to attach it to by hand.

  Worth knowing: no fully static web app can silently fire off an email on
  your behalf — browsers require a person to complete the final send/attach
  step for security reasons. This is the fastest version of that possible
  without standing up a backend and an email-sending service (e.g. via
  Brevo) to send automatically; that's a bigger, separate build if it's ever
  worth doing.

## Google Drive backup

Everything else in this app lives only in the browser that made it (see
"Data & privacy" below) — which is fine for drafts, but means a sent quote
saved on one phone doesn't exist anywhere else. Google Drive backup closes
that gap: once set up, every **Download PDF**, **Send to Customer**,
**Download Treasure Brief PDF**, and **Send My Estimate to Office**
silently uploads into two subfolders inside the Drive folder you chose:

- **PDFs** — the finished document itself, same as what got downloaded or
  sent
- **Quote Links** — a JSON snapshot of that quote's full data, kept in
  sync (overwritten in place, not duplicated) every time that quote backs
  up again

Those subfolders are created automatically the first time you back
something up — nothing to set up by hand. A small toast at the bottom of
the screen confirms each backup (or says if one failed) without
interrupting what you were doing; a failed backup never blocks the actual
download or send, it just means that copy is local-only until you
reconnect.

The Quote Links subfolder is what makes a quote genuinely reachable from
any device, not just backed up as a static file:

- **🔗 Copy Link** in the top bar copies a URL for the current quote
  (`?loadQuote=<reference>`). Opening that URL on any device signed into
  the same Drive folder loads that exact quote straight into the app,
  fully editable — checked locally first (instant, no network), then
  fetched from the Quote Links subfolder if it's not already on that
  device.
- The **Load saved quote** dropdown does the same merge automatically: it
  lists quotes saved on this device, plus — if Drive is connected — any
  quote backed up from another device that isn't already local, labelled
  "(from Drive)". Picking one of those fetches and caches it locally, so
  it's instant from then on.

This works from a plain static page because Google's own client-side
sign-in is the security boundary — nothing uploads until *you* sign in and
approve it, so unlike an AI API key there's nothing secret to leak. Setup
is one-time per Google Cloud project (not per device):

1. At **console.cloud.google.com**, sign in with your Google Workspace
   account and create a project (e.g. "Local Treasures Quote Tool").
2. **APIs & Services → Library** — enable **Google Drive API** and
   **Google Picker API**.
3. **APIs & Services → OAuth consent screen** — User Type **Internal**
   (only available on Workspace; means no Google review and no "unverified
   app" warning, restricted to your own domain's accounts). Fill in an app
   name and support email.
4. **APIs & Services → Credentials → Create Credentials → OAuth client ID**
   — type **Web application**, add this app's URL under "Authorized
   JavaScript origins" (e.g. `https://moosey88.github.io`). Copy the
   **Client ID**.
5. **APIs & Services → Credentials → Create Credentials → API key** — then
   restrict it: **HTTP referrers** matching this app's URL (e.g.
   `https://moosey88.github.io/*`), and **API restrictions** limited to
   **Google Picker API** only. Copy the **API key**.
6. In this app's **Settings → Google Drive Backup**, paste in the Client ID
   and API Key, Save, then click **🔗 Connect Google Drive** (Google
   sign-in popup) and **📁 Choose Drive Folder** (pick or create the folder
   quotes should land in — e.g. your existing Customer Quotes folder).

Each of those steps only needs doing once for the business, not per device
— from then on, anyone signing in from a new device just needs the Client
ID/API Key pasted into their Settings (the same two values every time) and
to Connect + Choose Folder on that device. The access token itself is never
stored — it's requested fresh (silently, no popup, if you signed in
recently) each time a PDF backs up, and kept in memory only.

Access is scoped to Google's `drive.file` permission — the narrowest Drive
scope there is. It only ever lets this app see files it creates itself, or
a folder you explicitly hand it through the picker; it cannot browse, read,
or touch anything else in your Drive.

## Data & privacy

Everything (quotes, photos, settings) is stored locally in the browser via
`localStorage` — nothing is sent anywhere unless you've set up Google Drive
backup above, in which case only the generated PDFs are uploaded, to the
folder you chose, using your own Google sign-in. Photos are embedded as
base64, so very large photo libraries across many quotes can bump up
against browser storage limits; keep images reasonably sized (a phone photo
is fine).
