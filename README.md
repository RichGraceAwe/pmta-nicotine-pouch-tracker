# PMTA Nicotine Pouch Tracker

> Open dataset tracking FDA PMTA (Premarket Tobacco Product Application) submission and marketing-authorization status for every major US nicotine pouch SKU.

**Last updated:** <!--LAST_UPDATED-->2026-09-15<!--/LAST_UPDATED-->
**SKUs tracked:** <!--SKU_COUNT-->63<!--/SKU_COUNT-->
**Live web view:** [cleannicotinepouch.com/fda-pmta-tracker](https://cleannicotinepouch.com/fda-pmta-tracker)

---

## What is this

A machine-readable snapshot of which nicotine pouch SKUs sold in the US market currently hold FDA marketing authorization through the PMTA pathway, which are still under review, and which have never submitted.

The PMTA process — created by the Family Smoking Prevention and Tobacco Control Act of 2009 — is the FDA's gatekeeper for any new tobacco / nicotine product. Marketing authorization status is the single most consequential regulatory fact about a nicotine pouch: it determines legal sale, retail distribution, and consumer trust. But this status is **not published in one consolidated place** by the FDA; it's scattered across press releases, marketing granted orders (MGOs), and the CTP product database.

This dataset consolidates the public-record status into one CSV / JSON file, updated as new decisions land.

## Why a separate repo

The dataset is also embedded in our live web tracker at [cleannicotinepouch.com/fda-pmta-tracker](https://cleannicotinepouch.com/fda-pmta-tracker) for human browsing. This repo exists so:

1. **Researchers** can pull the raw data without scraping HTML
2. **Journalists** writing about pouch regulation can cite a stable URL
3. **Other apps** can integrate the status as a JSON dependency
4. **Anyone correcting an error** can open a PR with citations, and we update both this repo and the live site

## Schema

| Field | Type | Description |
|---|---|---|
| `sku_name` | string | Canonical SKU name (e.g., `ZYN Cool Mint 6mg`) |
| `brand` | string | Brand name (e.g., `ZYN`, `VELO`, `Rogue`) |
| `manufacturer` | string | Legal manufacturer (e.g., `Swedish Match`) |
| `flavor` | string | Flavor descriptor (e.g., `Cool Mint`) |
| `strength_mg` | integer | Nicotine content per pouch in milligrams |
| `pouches_per_can` | integer | Standard can count |
| `format` | string | `Mini` / `Mini (dry)` / `Slim` / `Regular` |
| `status` | enum | `authorized` / `pending` / `denied` / `not-submitted` / `unknown` |
| `fda_status_raw` | string | Full status string with citation context |
| `tobacco_free` | boolean | `true` if non-tobacco-leaf product |
| `synthetic_nicotine` | boolean | `true` if uses synthetic (non-tobacco-derived) nicotine |
| `verified_source` | string | URL or citation reference for the status claim |

Full status-classification logic lives in [`scripts/export-pmta-tracker.mjs`](https://github.com/RichGraceAwe/cleannicotinepouch/blob/main/scripts/export-pmta-tracker.mjs) in our main repo.

## Files

```
data/
├── sku-pmta-status.csv     # primary export, comma-separated
├── sku-pmta-status.json    # same data, JSON, with metadata wrapper
```

The JSON wrapper includes top-level `updated`, `source`, and `count` fields plus a `skus` array of objects.

## How to use

### Read in Python

```python
import csv
with open('data/sku-pmta-status.csv') as f:
    skus = list(csv.DictReader(f))

authorized = [s for s in skus if s['status'] == 'authorized']
print(f"{len(authorized)} SKUs hold FDA marketing authorization")
```

### Read in Node.js

```js
import fs from 'fs';
const { skus } = JSON.parse(fs.readFileSync('data/sku-pmta-status.json', 'utf8'));
const byBrand = Object.groupBy(skus, (s) => s.brand);
```

### Read in R

```r
skus <- read.csv("data/sku-pmta-status.csv", stringsAsFactors = FALSE)
table(skus$status)
```

## Update frequency

We update this dataset whenever a new FDA decision is published or a brand makes a credible submission claim. Historical updates are tracked in [CHANGELOG.md](./CHANGELOG.md).

The web tracker at [cleannicotinepouch.com/fda-pmta-tracker](https://cleannicotinepouch.com/fda-pmta-tracker) is regenerated on every site build; this dataset typically lags by 0-7 days behind the live page.

## Contributing

Corrections and citations welcome. Open an issue or PR with:

1. The SKU name (exact)
2. The corrected field + value
3. A primary source (FDA notice, press release URL, or court filing). We don't accept secondhand reporting alone.

PRs that pass review will be merged here and synced to the live tracker at cleannicotinepouch.com on the next site build.

## License

This dataset is released under the **Creative Commons Attribution 4.0 International License** (CC BY 4.0). See [LICENSE](./LICENSE).

**Attribution:** If you use this data in a paper, article, or product, please cite:

> *PMTA Nicotine Pouch Tracker.* Maintained by [Clean Nicotine Pouch](https://cleannicotinepouch.com). Retrieved from `https://github.com/<owner>/pmta-nicotine-pouch-tracker`.

## Disclaimer

This dataset is provided for informational and research purposes. Nothing here constitutes legal advice, medical advice, or a marketing authorization claim. The authoritative source for FDA PMTA decisions is the [FDA Center for Tobacco Products](https://www.fda.gov/tobacco-products). Where this dataset and an FDA primary source disagree, the FDA source controls.

Nicotine is an addictive chemical. Products covered by this dataset are intended for adults 21 and older.

## Maintainers

[Clean Nicotine Pouch](https://cleannicotinepouch.com) — independent nicotine pouch reviews, comparisons, and regulatory tracking.
