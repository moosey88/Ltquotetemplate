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
- Site/reference photos with captions — attach what you saw on the visit
- Line items table (description, qty, unit price) with an auto-calculated total
- Discount — quick 5/10/15% buttons, or a custom % or £ amount with a reason,
  applied to the subtotal before deposit/total
- Deposit % and total, calculated live
- Terms & conditions text
- Footer with your contact and bank details (from Settings)

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
details, and the defaults that get pre-filled on every new quote (deposit %,
fee %, quote validity in days, default terms, default project comments).

## Saving & sending

- **Save** stores the current quote in the browser (localStorage) so you can
  come back to it later via the **Load saved quote** dropdown.
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

## Data & privacy

Everything (quotes, photos, settings) is stored locally in the browser via
`localStorage` — nothing is sent anywhere. Photos are embedded as base64, so
very large photo libraries across many quotes can bump up against browser
storage limits; keep images reasonably sized (a phone photo is fine).
