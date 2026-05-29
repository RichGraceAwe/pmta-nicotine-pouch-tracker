# Dataset Schema

See [`../README.md`](../README.md) for the full schema description.

## Files

- `sku-pmta-status.csv` — CSV export, one row per SKU. UTF-8.
- `sku-pmta-status.json` — JSON export with `{ updated, source, count, skus: [...] }` envelope.

## Status enum values

| Value | Meaning |
|---|---|
| `authorized` | The SKU holds an active FDA Marketing Granted Order (MGO) under PMTA. |
| `pending` | A PMTA has been submitted and is under FDA review. No authorization yet. |
| `denied` | The FDA has issued a Marketing Denied Order (MDO). The SKU may still be sold during appeal. |
| `not-submitted` | No PMTA has been submitted to the FDA. |
| `unknown` | Status could not be reliably determined from public sources. |

## Boolean conventions

`tobacco_free` and `synthetic_nicotine` are JSON booleans (`true` / `false`). In CSV they appear as the literal strings `true` / `false`.

## Empty values

CSV empty cells and JSON `null`/`""` indicate the field is not applicable or not yet confirmed (e.g., a manufacturer not yet published).
