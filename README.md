# Bloom — Medication Companion (PWA)

A small installable web app for personal medication scheduling, package-aware stock forecasting, cost comparisons, and a private progress journal. Purple, soft, and mobile-friendly.

## Deploy to Netlify
1. Unzip this folder.
2. In Netlify, choose **Add new site → Deploy manually** and drag the folder contents (or connect the repository).
3. Open the HTTPS site in Chrome. Tap the install icon in the address bar or use Chrome menu → **Install app**.

## Deploy to GitHub Pages
1. Create a repository and upload all files in this folder to the repository root.
2. Open **Settings → Pages**, choose the branch and root folder, and save.
3. Open the published HTTPS URL in Chrome and install it.

## Included
- PWA manifest, service worker, SVG icon.
- Password-based encryption of saved app data using Web Crypto (PBKDF2 + AES-GCM).
- Active medicine list: schedule days, multiple times, fractional dose amounts (e.g. 0.5 or 0.25 units), opened-package remainder, unopened package count, low-stock threshold, and package pricing.
- Medicine form types: tablet/pill, gel, or other. For gel, use a consistent stock/dose unit such as grams or pumps.
- Package pricing: enter units per box/tube/pack and package price, or enter the individual unit price. Package price takes precedence when entered and package size is valid; monthly cost uses the calculated unit price. Restocking can add unopened packages or loose/opened units. Total stock is calculated automatically.
- Estimated run-out date and monthly cost; display costs in THB or USD using a user-entered exchange rate.
- Considering list for comparing monthly cost of candidate medicines with one active medicine or all active medicines combined. Candidate medicines do not affect the active schedule or stock.
- Progress journal with dated notes, optional weight/measurement notes, and resized photo attachments stored inside encrypted app data.
- Optional photo attached directly to each medication record, with preview and remove controls.
- Daily checklist for schedule items.
- Foreground browser notifications at scheduled dose times while the app is open and visible (not guaranteed after closing the app/browser).
- Forecasts that simulate the actual entered schedule day-by-day, show an estimated refill-threshold date, and optionally include medicine-level reserve quantity in the run-out estimate.
- Corrected monthly cost estimate for daily, weekday, weekend, and custom-day schedules.

## Important limitations
- This is a tracking tool, not a prescribing or dose-calculation tool. Enter only the regimen given by your clinician. It does not decide which medicine you should take.
- Stock forecasts simulate the entered days and dose amounts day-by-day. They assume the schedule is followed and stock is measured in the same unit as each dose. You can choose whether the reserve quantity entered on a medicine is included in its run-out forecast. Items in the separate Reserve shelf remain inventory notes until moved into a matching medicine’s current stock. Forecasts do not account for missed doses, prescription changes, pill splitting, or expiry unless you update the data.
- Monthly cost is estimated from the entered schedule, unit price, or package price. It does not model discounts, changes in prices, or currency-rate changes unless you update the details.
- Scheduled browser notifications are checked while Bloom is open and the page is visible. The app does **not** guarantee alarms when closed or suspended by the operating system. Keep a separate reliable reminder for time-critical medication.
- Data is stored locally in the current browser profile. Clearing site data, changing browser/profile, or uninstalling may remove access. Export backups regularly.
- The password lock protects casual access and encrypts app data at rest, but does not secure the device itself. If you forget the password, encrypted data cannot be recovered. Backups are encrypted with the same password.
- HTTPS is required for Web Crypto and PWA installation. Netlify and GitHub Pages provide HTTPS.
- The first visit may need internet access to load the Google Fonts stylesheet; the app itself uses a system fallback font offline.

## Before using
Test adding/editing/deleting a sample medicine, the schedule day calculation, stock adjustments, backup restore, and install behavior on your own phone. Do not put identifying information in medicine notes if you share screenshots.


## Updated inventory, comparison, and progress features

- **Automatic current stock:** enter units remaining in the opened package and the number of unopened packages. Total stock is calculated as opened/loose units plus unopened packages multiplied by package size. Logging a dose opens a new package automatically in the calculation when needed.
- **Considering / cost comparison:** add medicines you may discuss with your clinician without activating them in the dose schedule. Enter package size, package price, expected units used per scheduled day, and schedule days to estimate monthly cost. Compare against one active medicine or all active medicines combined. This is a cost estimate only, not a dose-equivalence or treatment recommendation.
- **Progress journal and medication photos:** add a photo to a dated progress entry or directly to a medication record. Images are resized before storage and included inside the encrypted backup. Image pickers use `accept="image/*"` without a forced `capture` attribute, allowing supported mobile browsers to offer the camera and existing photos/files. The exact chooser options depend on the device and browser. Browser storage is limited; export backups regularly, especially if saving many photos.
- **GitHub Pages identity:** the manifest uses `/Medic/` for its app ID, start URL, scope, and icon path. Change these paths if deploying to a different repository path. The service worker cache version was incremented so updated files can replace the older cached version.


## Compact interface update (v7)
- Medication list uses a compact three-column square-tile grid with tag-specific colors.
- Tag filters are horizontal chips instead of a dropdown.
- Tag creation and management moved to More → Tags; settings moved to More → Settings & backup.
- Main navigation is five equal-width tabs and no longer requires horizontal swiping.


## Look & feel update (v8)
- **5 colour themes:** Lavender, Rose, Ocean, Sage and Midnight (dark). Choose in More → Theme, or tap the palette button in the top bar to cycle. The choice is remembered on the device and applied before the page paints (no flash).
- **Easier scrolling:** bottom navigation bar with icons (always in thumb reach), sticky header, one-row swipeable tag filter that stays pinned, floating "Add" button on Medicines / Compare / Progress, and forms that open as bottom sheets on phones with a pinned Save button.
- **Today:** doses grouped into Morning / Afternoon / Evening, large tap-anywhere tick circles, and a progress ring showing doses done.
- **Medicines:** switch between Tiles and List views (remembered).
- **Fix:** Edit buttons on progress entries now open the editor only when tapped.
- Add a new theme by adding one `:root[data-theme="name"]{...}` block in styles.css and one entry in the `THEMES` array at the bottom of app.js.
