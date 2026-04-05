# Genuity evidence-first industrial reconciliation run

## Outcome

- Ten required behaviours: **FAIL**
- Documents/pages processed: **12**
- Existing OCR results consumed: **12**; incremental OCR calls: **0**
- Automatically accepted fields: **83**
- Evidence coverage of accepted fields: **100.0%**
- Critical-field fixture precision/automatic coverage: **23.1% / 21.4%** across **28** fields
- External regions routed: **0** (0.00% of pages)
- Model-result cache hits: **0**
- Human-review cases: **6**
- Unresolved fields: **3**
- Estimated selective-pipeline batch cost: **$6.7682**
- Cost-per-verified-field saving vs full-page VLM scenario: **49.45%**
- Provenance integrity checks: **21/21 PASS**
- Operational release: **REVIEW_REQUIRED**; write-back allowed: **false**

## Connected answer

`PO:LTTS-PO-2024-0847 -> PART:PN-304L-PLT-0750 -> BOM:BOM-HDS-304L-R2 -> SPEC:SPEC-SA240-304L:R2 -> CERT:NAS-893611 -> HEAT:AN4T -> TEST:CHEM-AN4T -> TEST:MECH-AN4T`

The material certificate is linked through the CoC certificate number and shared heat/part evidence. Displayed chemistry passes the latest displayed specification. Invoice quantity 44 conflicts with PO quantity 45 and is not silently resolved. Certificate boron 0.0002 is only a proposal from the same-heat ladle table. The missing hardness cell is a 39.0 HRC analytics-only median. Inspector signoff remains `UNRESOLVED`.

## Safety and cost notes

The demo VLM adapter is simulated and sees only one crop. Its candidate is not auto-accepted. `operational_release.json` blocks system-of-record write-back while safety exceptions or scoped approvals remain. Pricing is dated `2026-08-16` and human/token assumptions are explicit in `cost_report.json`; they are planning estimates, not invoices.
