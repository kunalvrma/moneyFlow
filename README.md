# moneyFlow

A minimal, mobile-first transaction logger that submits directly to a Google Sheet via Google Forms — no app, no backend, no login.

Built to replace the friction of opening Google Forms on mobile. One screen, large tap targets, done in under 10 seconds.

---

## Features

- **One-screen UI** — no multi-step sections, everything visible at once
- **OUT pre-selected by default** — optimised for the most frequent use case
- **15 categories** as a tap grid — no scrolling, no dropdowns
- **TRANSFER flow** — shows destination account only when needed
- **Add to Home Screen** — works as a standalone app on iOS and Android
- Writes directly to Google Sheets via form submission

---

## Stack

Pure HTML + CSS + Vanilla JS — no frameworks, no dependencies, no build step.

Fonts via Google Fonts (DM Mono + Syne). Submissions via hidden iframe POST to Google Forms.

---

## Setup

This repo is personal and tied to a specific Google Form and Sheet. To adapt it for your own use:

1. Create your own Google Form with these fields:
   - Account *(radio)*
   - Flow Type *(radio)*
   - Amount *(short answer)*
   - Destination Account *(radio — Section 2)*
   - Category *(radio — Section 3)*
   - Description *(short answer — Section 3)*
   - Person / Tag *(short answer — Section 3)*

2. Get your form's entry IDs from the Network tab (DevTools → submit once → Payload)

3. Replace the `entry.XXXXXXXXX` values and form action URL in `index.html`

4. Deploy via GitHub Pages

---

## Add to Home Screen

**iOS (Safari):** Share → Add to Home Screen

**Android (Chrome):** Menu → Add to Home Screen

Opens full-screen, no browser UI, behaves like a native app.

---

## Notes

- The form is public on GitHub Pages but the Sheet is private — no data is exposed
- Ad blockers (uBlock Origin etc.) can interfere with form POST — disable for the GitHub Pages domain
- `pageHistory` must be set correctly for multi-section Google Forms or Section 3 fields will be silently dropped

---

## License

Personal project. No license — not intended for redistribution.
