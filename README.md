# Which Card?

A one-page, phone-friendly guide to which credit card to use for each purchase
(Discover it, Amex Blue Cash Preferred, Chase Sapphire Preferred).
Works offline and can be added to your phone's home screen.

## Host it on GitHub Pages

1. On github.com, click **New repository** → name it (e.g. `which-card`) → **Create repository**.
2. Click **uploading an existing file**, drag in everything from this folder
   (`index.html`, `manifest.json`, `sw.js`, `icon.svg`, `icon-*.png`, `.nojekyll`, `README.md`) → **Commit changes**.
   Tip: `.nojekyll` is a hidden file; if you can't see it, skip it — the site still works.
3. Go to **Settings → Pages**. Under **Build and deployment**, set Source = **Deploy from a branch**,
   Branch = **main**, folder = **/ (root)** → **Save**.
4. After about a minute your site is live at `https://<your-username>.github.io/which-card/`.

## Put it on your phone's home screen

- **iPhone (Safari):** open the link → Share button → **Add to Home Screen**.
- **Android (Chrome):** open the link → ⋮ menu → **Add to Home screen** / **Install app**.

It opens full-screen like an app and works without signal after the first visit.

## Updating it each quarter (2 minutes)

The site reads today's date, so it switches Discover's 5% categories on its own —
you only need to add each new quarter once Discover announces it (usually mid-month before).

1. On GitHub, open `index.html` → pencil icon (Edit).
2. Near the top, find `DISCOVER_QUARTERS` and add a line, e.g.
   `'2027-Q1': { label: 'Grocery stores, streaming', cats: ['groceries', 'streaming'] },`
   Category ids you can use: groceries, dining, delivery, gas, streaming, utilities,
   entertainment, transit, lyft, travel, rentals, warehouse, shopping, drugstore, home,
   bigticket, abroad, other.
3. Open `sw.js` and bump `VERSION` (e.g. `v3-2027-01-01`) so phones fetch the new copy.
4. Commit — GitHub republishes automatically.

Until a quarter is added, Discover shows 1% everywhere and the Activate tab lists it as
"categories not announced yet".

## Calendar reminders

The **Activate** tab has an "Add reminders to my calendar" button (`reminders.ics`):
Discover activation every Mar 15 / Jun 15 / Sep 15 / Dec 15, the Chase Apple TV deadline,
and a monthly nudge to use the $10 DoorDash promo.

## Privacy note

GitHub Pages sites on free accounts are public. This page contains no card numbers or
account info, and a `noindex` tag keeps search engines from listing it — but anyone with
the link can open it.
