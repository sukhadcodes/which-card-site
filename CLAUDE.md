# Which Card? — maintenance instructions

Static, single-page site (GitHub Pages, branch `main`, root). Personal credit-card guide for
three cards: Discover it Cash Back, Amex Blue Cash Preferred, Chase Sapphire Preferred.
No build step — edit files and push to `main`; Pages republishes in ~1 minute.

## Files
- `index.html` — everything. All data lives in the `EDIT HERE` block at the top of the `<script>`:
  - `DISCOVER_QUARTERS` — Discover 5% calendar, keyed `'YYYY-Qn'`.
  - `CHASE_CPP` — cents per Chase point used for ranking (default 1.25).
  - `CATEGORIES` — per-category rates for each card: `[shown rate, cash-equivalent %, note]`.
  - `ACTIVATIONS` — Activate-tab items per card (`once`, `monthly`, `due`, `info`, `date`).
- `sw.js` — offline cache. **Bump `VERSION` on every content change** (format `vN-YYYY-MM-DD`),
  otherwise installed phones keep the old copy.
- `reminders.ics` — calendar reminders (rarely changes).
- `README.md` — user-facing setup/update notes.

## Quarterly Discover update
1. Find the newly announced Discover 5% categories from an official source
   (discover.com cashback calendar) or confirm with two reputable sites. Never guess.
2. Add one entry to `DISCOVER_QUARTERS`, e.g.
   `'2027-Q1': { label: 'Grocery stores, wholesale clubs', cats: ['groceries', 'warehouse'] },`
   Map each Discover category to existing ids only:
   groceries, dining, delivery, gas, streaming, utilities, entertainment, transit, lyft, travel,
   rentals, warehouse, shopping, drugstore, home, bigticket, abroad, other.
   If a Discover category has no matching id (e.g. "PayPal", "digital wallets", "Amazon.com"),
   map it to the closest one (Amazon.com → shopping) and mention it in `label`; if nothing fits,
   add a new `CATEGORIES` entry following the existing format.
3. Bump `VERSION` in `sw.js`.
4. Verify: open `index.html` headless (Playwright, ~390px wide), no console errors, the grid
   loads, and the Activate tab renders.
5. Commit to `main` with a message like `Discover 2027 Q1: grocery stores, wholesale clubs`.

## Annual review (January)
Re-check each card's official page for changes to earning rates, caps, fees, credits,
enrollment deadlines and promo end dates. Update `CATEGORIES`, `ACTIVATIONS`, the Tips tab
and the "Info as of" date in the footer. Remove expired one-time items. Bump `VERSION`.
Anything ambiguous (e.g. a card was renamed or converted by the issuer): don't guess —
report it instead of committing.

## Rules
- Keep the site self-contained: no external scripts, fonts or trackers.
- Never add personal or account data (card numbers, balances, names).
- Keep `<meta name="robots" content="noindex">`.
