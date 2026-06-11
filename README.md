# moneyFlow

A minimal, mobile-first transaction logger that submits directly to a Google Sheet via Google Forms -- no app, no backend, no login.

Built to replace the friction of opening Google Forms on mobile. One screen, large tap targets, done in under 10 seconds.

---

## Features

- **One-screen UI** -- no multi-step sections, everything visible at once
- **OUT pre-selected by default** -- optimized for the most frequent use case
- **15 categories** as a tap grid -- no scrolling, no dropdowns
- **TRANSFER flow** -- shows destination account only when needed
- **Description chips** -- remembers frequent descriptions by flow, account, and category
- **Add to Home Screen** -- works as a standalone app on iOS and Android
- Writes directly to Google Sheets via form submission

---

## Description Chips

Description suggestions are stored in `localStorage` under `mf_sugg`.

Each successful log entry saves the description against this key shape:

```text
Flow Type|Account|Category
```

Example:

```text
OUT (-)|Kotak811|Vice
```

When a category is selected, the HUD shows the top 5 most-used descriptions for that exact flow/account/category combo. Tapping a chip fills the description field instantly.

The suggestion pool is capped at the top 20 descriptions per combo, so browser storage stays small.

This version also includes a one-time historical seed generated from the form responses sheet:

- 831 usable historical descriptions
- 73 flow/account/category combos
- Seed flag: `mf_sugg_seed_v1`

The seed only runs once per browser profile. New entries continue to improve the same `mf_sugg` data after that.

---

## Stack

Pure HTML + CSS + Vanilla JS -- no frameworks, no dependencies, no build step.

Fonts via Google Fonts (DM Mono + Syne). Submissions via hidden iframe POST to Google Forms.

---

## Setup

This repo is personal and tied to a specific Google Form and Sheet. To adapt it for your own use:

1. Create your own Google Form with these fields:
   - Account *(radio)*
   - Flow Type *(radio)*
   - Amount *(short answer)*
   - Destination Account *(radio -- Section 2)*
   - Category *(radio -- Section 3)*
   - Description *(short answer -- Section 3)*
   - Person / Tag *(short answer -- Section 3)*

2. Get your form's entry IDs from the Network tab:
   DevTools -> submit once -> Payload

3. Replace the `entry.XXXXXXXXX` values and form action URL in `index.html`

4. Deploy via GitHub Pages

---

## Deploy

This project is designed to run directly from GitHub Pages.

For a simple update:

```powershell
git add index.html README.md
git commit -m "Seed description chips from form history"
git push
```

If this is the first push from a fresh local clone:

```powershell
git remote add origin https://github.com/kunalvrma/moneyFlow.git
git branch -M main
git push -u origin main
```

---

## Add to Home Screen

**iOS (Safari):** Share -> Add to Home Screen

**Android (Chrome):** Menu -> Add to Home Screen

Opens full-screen, no browser UI, behaves like a native app.

---

## Notes

- The form is public on GitHub Pages but the Sheet is private -- no data is exposed
- Ad blockers such as uBlock Origin can interfere with form POST -- disable for the GitHub Pages domain
- `pageHistory` must be set correctly for multi-section Google Forms or Section 3 fields will be silently dropped
- To re-run the historical chip seed in the same browser, delete `mf_sugg_seed_v1` from localStorage first

---

## License

Personal project. No license -- not intended for redistribution.
