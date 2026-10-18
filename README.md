# Ex-Track

**A boring vibe coded expense tracker.**

Type an amount, pick a category, tap Save. That's it. Ex-Track shows what you spent this month and how much budget is left, nothing more.

- Plain HTML, CSS and JavaScript in one file, with no framework and no build step
- About 8 KB compressed, and works offline
- 100% local: no account, no server, no tracking

## Install

**iPhone (Safari)**
1. Open the app's address in Safari.
2. Tap **Share → Add to Home Screen**.
3. From now on, always open Ex-Track from the home screen icon. Safari and the installed app keep separate data.

**Android (Chrome)**
1. Open the app's address in Chrome.
2. Tap **⋮ → Add to Home screen** (or **Install app**).
3. Open Ex-Track from the new icon.

## How it works

- **Log:** type an amount, pick a category, Save. Choose **Other** to give it your own name.
- **Edit:** tap an expense. **Delete:** swipe it left. Both can be undone right away.
- **Budget:** tap **Set budget** once. The bar and "left" amount only show for the current month.
- **Breakdown:** tap the chart icon to see spending per category.
- **Months:** use ‹ › or swipe across the header.

## How the data is stored

Everything lives in your browser's IndexedDB, on your phone only. Each expense is one small record of about 50 bytes:

```js
{ id: 1760766000000, a: 25000, c: 0, d: 20261018, n: "Parking" }
```

| Field | Meaning |
| --- | --- |
| `id` | Time it was created, used as a unique key |
| `a` | Amount in rupiah |
| `c` | Category number (0 = Food … 6 = Other) |
| `d` | Date as `YYYYMMDD` |
| `n` | Custom name, only for Other |

An index on `d` lets the app read just the month on screen, so it stays fast after years of use. The monthly budget is a single number in `localStorage`. The app asks the browser for persistent storage, so the data isn't cleared to save space.

**Heads-up:** removing the app or clearing site data deletes your expenses. There is no backup yet.

## Files

| File | Purpose |
| --- | --- |
| `index.html` | The whole app |
| `manifest.webmanifest` | App name, colors and icons for installing |
| `sw.js` | Service worker that caches the app for offline use |
| `icons/` | App icons |

To ship an update, bump the cache name at the top of `sw.js` (e.g. `ex-track-v1` → `ex-track-v2`) so installed apps pick up the new version.
