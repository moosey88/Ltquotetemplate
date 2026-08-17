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
- **Print / PDF** opens the browser print dialog with the internal tab and
  all app chrome hidden — "Save as PDF" gives you a clean customer-facing
  document.
- **Email** opens your default mail client with a plain-text summary of the
  quote pre-filled, addressed to the customer's email. Attach the printed
  PDF manually if you want the formatted version with photos.

## Data & privacy

Everything (quotes, photos, settings) is stored locally in the browser via
`localStorage` — nothing is sent anywhere. Photos are embedded as base64, so
very large photo libraries across many quotes can bump up against browser
storage limits; keep images reasonably sized (a phone photo is fine).
