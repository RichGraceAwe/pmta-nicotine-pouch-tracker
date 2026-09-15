# Changelog

All notable updates to the PMTA nicotine pouch dataset are recorded here.

The format is loosely based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).
Dates are ISO-8601 (YYYY-MM-DD).

## 2026-09-15

- 63 SKUs (was 48). Status breakdown: 43 authorized, 20 pending, per FDA's authorized-products list current through 2026-08-21.
- Added: 11 ZYN Ultra products authorized 2026-08-21 (ten flavors at 9mg, Smooth at 11mg), listed under FDA's product names; 6 original-line on! products (Autumn Spice, Cappuccino, Rich Berry at 2mg and 4mg) that appear on FDA's list; Rogue Apple 3mg/6mg; Lucy Mango 12mg.
- Removed: SKUs the brands do not sell in the US, checked against velo.com/us, onnicotine.com, lucy.co and roguenicotine.com (VELO Ice Cool 4/7mg, VELO Bahia Breeze 4mg, on! PLUS Mint 3mg, Lucy Pomegranate 12mg, five VELO 11mg rows).
- Corrected: Rogue `synthetic_nicotine` is now `false` (Rogue's help center: nicotine is steam-extracted from tobacco leaf and bound as nicotine polacrilex); Rogue manufacturer is Rogue Holdings, LLC (Swisher); Lucy "Cool Mint" renamed "Mint" and VELO "Dryft Spearmint" renamed "Spearmint" to match the brands' names; `verified_source` now carries the official-site URL used for each row.
- Note: Lucy and FRE `synthetic_nicotine` flags are carried over from earlier research; neither brand states the nicotine source on its official site.

## 2026-05-29

- Initial public release.
- 48 SKUs across 6 brands: ZYN, VELO, Rogue, on! PLUS, Lucy, FRE.
- Status breakdown reflects FDA decisions through May 2026, including the January 2025 ZYN authorization and the on! PLUS line.
- Dataset and web view ([cleannicotinepouch.com/fda-pmta-tracker](https://cleannicotinepouch.com/fda-pmta-tracker)) are kept in sync via `scripts/export-pmta-tracker.mjs` in the main site repo.
