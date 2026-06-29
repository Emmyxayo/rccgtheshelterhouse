# RCCG The Shelter — Website

Single-page site for RCCG The Shelter, Okota. Built to deploy free on GitHub Pages.

## Structure
- `index.html` — the whole site (HTML/CSS/JS in one file)
- `images/` — logo + optimised photos (kept as separate files so the HTML stays small)

## Deploy on GitHub Pages
1. Create a repo (e.g. `theshelter`) and upload `index.html` + the `images/` folder (keep the folder structure).
2. Repo **Settings → Pages → Source: main branch / root**.
3. Your site goes live at `https://<username>.github.io/theshelter/`.

## Before going live — fill these in
- **Giving section:** account name / bank / account number, and your Paystack payment link
  (search `payBtn` and the `[ Add ... ]` placeholders in `index.html`).
- Confirm the **YouTube / Mixlr / Instagram** links are correct.
- Optional: swap the nav logo chip for a transparent PNG if you have one (`images/logo.png` is a generated transparent version).

## Notes
- Brand colours are pulled straight from the logo (indigo + the five shelter colours).
- The five-arch motif in the hero/footer is drawn in SVG (no image needed).
- Map, WhatsApp, tel and email links are all live.
