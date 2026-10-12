# Aerospace MTR Validation Demo (LTTS context)

Demonstration of document-trust reconciliation on an aerospace MTR chain:
12 SA-240 304L documents reconciled into database-ready records. Built by
Genuity IO; the reconciliation engine behind it lives in
[genuity-reconcile](https://github.com/AK47-1845/genuity-reconcile).

## What's inside

- `LTTS_DEMO_DASHBOARD.html` — open in a browser: the demo dashboard.
- `LTTS_PITCH_DECK.md` / `.html` / `.pptx` — pitch narrative in three formats.
- `LTTS_DEMO_PRESENTATION.md` — demo script.
- `ltts_sa240_304l_domain_pack.json` — the domain pack (grades, specs, rules).
- `ocr_packet/` — sample OCR inputs; `genuity_output/` — reconciled outputs.
- `MTR Validation.pdf` — writeup; `monday.md` — working notes.

## Result (measured, demo scope)

12-document SA-240 304L chain reconciled in under a second on the demo
machine. Scope honesty: this demonstrates the pipeline on one document
family — it is not a claim about all MTRs, all mills, or production
deployment.

## View it

No install: download and open `LTTS_DEMO_DASHBOARD.html`. To run the engine
itself, see [genuity-reconcile](https://github.com/AK47-1845/genuity-reconcile).

> "Validation has to be re-earned for every physical environment, not claimed
> once and reused."
