# YCC Compass — Marketplace Prototype

A visual concept prototype for **YCC Compass**, a one-stop student marketplace covering
admissions tracking, scholarship discovery, test prep, document tools, and a role-based
login for students, guardians, counsellors, and employers.

## What's in this repo

- **`index.html`** — the marketing/landing page: hero, module grid, role-based dashboard
  preview, pricing, and the employer/visa section.
- **`scholarship-radar.html`** — a deep-dive screen for the Scholarship Radar module:
  filters, match-% scoring, deadline urgency bars, and the "why does this match me?"
  breakdown.

Both files are **plain HTML, CSS, and vanilla JavaScript** — no framework, no build step,
no dependencies. Open either file directly in a browser and it works as-is.

## What's real vs. placeholder

This is a **visual and interactive prototype**, not a working application. Specifically:

- All scholarship listings, deadlines, match percentages, and dashboard numbers are
  **hard-coded sample content**, not live data.
- The role chips, tabs, save buttons, and match-breakdown toggles are functional
  JavaScript interactions — they do work — but nothing is saved anywhere; refreshing the
  page resets everything.
- The Facebook Group link in the footer is live. The "YCC App" footer link is currently a
  placeholder (`#`) pending the actual URL.
- Login buttons, search, and most CTAs are non-functional placeholders (`href="#"`).

## Deploying this prototype

1. Push both HTML files to a GitHub repo (this README included).
2. In the repo's **Settings → Pages**, set the source to the `main` branch, root folder.
3. GitHub will publish it at `https://<your-username>.github.io/<repo-name>/`.

No build step is required — GitHub Pages serves the HTML files directly.

## Files added for Android packaging

- **`manifest.json`** — PWA manifest (app name, colors, icons) required before this can be
  packaged as an Android app.
- **`service-worker.js`** — minimal offline caching for the app shell.
- **`about-ycc.html`** — the YCC consultancy's own content (credentials, services, contact),
  now linked from the footer and nav so the app includes the business itself, not just the
  marketplace tool.
- **`icon-192.png` / `icon-512.png` / `icon-maskable-512.png`** — app icons in the sizes
  Android and the Play Store require.

See the chat for the full step-by-step on turning this into a signed `.aab` via PWABuilder
and submitting it through Google Play Console.

## Advertising / monetization provision

Ad placeholder slots are wired into `index.html` (below the hero) and `scholarship-radar.html`
(in the feed) — dashed boxes marked "ADVERTISEMENT" that you can replace with a real ad
network's embed code once you're approved.

**Important technical note:** because this app is packaged for the Play Store as a
**Trusted Web Activity** (your website shown full-screen inside an Android shell — see
below), ads have to be **web-based ad units** embedded directly in the HTML, such as
Google AdSense, rather than a native mobile SDK like AdMob. AdMob requires native Android
code, which a TWA doesn't have. If you later rebuild this as a true native or React Native
app, native AdMob becomes an option — for now, a web ad network is the correct fit for the
architecture.

`privacy-policy.html` — the mandatory Play Store privacy policy, drafted to cover account
data, scholarship-matching profile data, and advertising identifiers. **This is a starting
draft, not legal advice** — have it reviewed before publishing, especially the advertising
and under-18 sections given the student audience.

## Building the real product

Once you're ready to move past the prototype, this will need an actual backend to store
student profiles, scholarship listings, and login sessions — plain HTML/JS can't do that
on its own. The recommended path is **React + Vite**, matching the stack already used for
the YCC Admission Compliance Ledger, deployed the same way (Netlify with a serverless
function proxy). That keeps one tech stack across the YCC product suite instead of
introducing a second one, and the two apps can eventually share a student-record backend.

Suggested build order:
1. Define the shared student-record data model (used by all four roles).
2. Rebuild this prototype's UI as React components on Vite.
3. Add real authentication and role-based routing.
4. Connect the Scholarship Radar to a real, counsellor-curated data source.
5. Add the AI match-scoring and explanation layer (Claude API).
