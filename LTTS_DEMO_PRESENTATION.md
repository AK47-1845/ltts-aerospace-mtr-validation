# 🏭 Genuity 2.0 — Live MTR Validation Demo for LTTS
## Presented to: Global AI Head, L&T Technology Services
## Date: August 17, 2026

---

# 1. THE PROBLEM WE SOLVE

> **Today at LTTS, when a steel plate arrives at a refinery project site, a Quality Engineer manually opens 8-12 PDF documents (Purchase Order, Invoice, MTR, Specification, BOM, CoC, Inspection Report) and cross-checks hundreds of data points by hand.**

### What goes wrong today:
- ❌ **OCR errors**: A part number `PN-304L-PLT-0750` gets misread as `PN-3O4L-PLT-O750` (letter O instead of zero) — and nobody catches it
- ❌ **Missing data**: Invoice doesn't print the part number — engineer has to manually look it up from the PO
- ❌ **Quantity conflicts**: PO says 12 plates, Invoice says 11 — which is right?
- ❌ **Unit confusion**: Tensile strength printed as 94,720 "MPa" when it's actually in PSI — wrong unit loaded into QMS
- ❌ **Obsolete specs**: Old revision of the specification accidentally used for validation
- ❌ **Duplicate scans**: Same certificate scanned twice at the receiving dock — double-counted
- ❌ **Missing signatures**: Inspection report not signed — but material gets released anyway

**Each of these errors costs $5,000–$50,000+ in rework, recalls, or compliance violations.**

---

# 2. WHAT GENUITY DOES (IN 30 SECONDS)

> Genuity sits **after** your existing OCR/extraction. It takes the extracted data from all documents in a procurement chain and automatically:

```
Step 1: CLASSIFY   → What type of document is this? (PO, Invoice, MTR, etc.)
Step 2: NORMALIZE  → Fix OCR errors, convert units, standardize material grades
Step 3: LINK       → Connect PO → Part → BOM → Spec → MTR → Heat → Test Results
Step 4: VALIDATE   → Check chemistry against spec limits, verify math
Step 5: CONFLICT   → Catch disagreements between documents
Step 6: DECIDE     → Accept (with evidence) or Block (for human review)
```

**Genuity never guesses. If it can't prove something, it stops and asks a human.**

---

# 3. LIVE DEMO: REAL SA-240 304L STEEL PLATE FOR JAMNAGAR REFINERY

## 3.1 The Scenario

We simulated a real procurement chain for **SA-240 Type 304L stainless steel plates** being procured from **North American Stainless (NAS)** for the LTTS Jamnagar Refinery HDS Unit reactor vessel shell.

### Documents Fed Into Genuity:

| # | Document | Source | Key Data |
|---|----------|--------|----------|
| 1 | **Purchase Order** | LTTS Procurement | PO: LTTS-PO-2024-0847, Qty: **12**, Part: PN-3**O**4L-PLT-**O**750 (OCR error) |
| 2 | **Supplier Invoice** | NAS Billing | PO: LTTS-PO-2024-0847, Qty: **11** (mismatch!), Part: **missing** |
| 3 | **Bill of Materials** | LTTS Engineering | Part: PN-304L-PLT-0750, Spec: SPEC-SA240-304L |
| 4 | **Material Specification** | ASME SA-240 Rev 2 | Cr: 18.00-20.00%, Ni: ≥8.00%, Tensile: 485-690 MPa |
| 5 | **Material Test Report (MTR)** | NAS Lab (Heat AN4T) | Cr: 18.211%, Ni: 8.078%, Boron: **blank**, Tensile: **stamp obscured** |
| 6 | **Certificate of Conformance** | NAS Quality | Links PO → Certificate → Heat |
| 7 | **Ladle Chemistry** | NAS Melt Shop | Same heat AN4T, Boron: 0.0002% |
| 8 | **Mechanical Properties** | NAS Lab | Tensile: 94,720 "MPa" (actually PSI — **unit error**) |
| 9 | **Hardness Table** | NAS Lab | 8 of 9 readings clear, 1 **smudged** |
| 10 | **Duplicate Scan** | Receiving Dock | Same certificate re-scanned by mistake |
| 11 | **Old Spec (Rev 1)** | Archive | **Superseded** — should not be used for validation |
| 12 | **Final Inspection** | LTTS QA | Inspector signoff: **not signed yet** |

> **NOTE: The chemistry values (Cr: 18.211%, Ni: 8.078%, Mo: 0.277%) are real values extracted from actual NAS MTR certificate #893611, Heat AN4T, from the open-source sample dataset.**

---

## 3.2 What Genuity Found Automatically (< 1 second processing time)

### ✅ AUTOMATICALLY ACCEPTED: 83 fields with 100% evidence coverage

| What Genuity Did | Detail | Business Impact |
|---|---|---|
| **OCR Error Fixed** | Part number `PN-3O4L-PLT-O750` → `PN-304L-PLT-0750` (matched against allowed parts registry) | Prevented wrong part being loaded into ERP |
| **Missing Part Number Recovered** | Invoice had no part number → Genuity borrowed it from PO after matching PO# and Supplier name | Saved 5-10 min manual lookup |
| **Total Amount Calculated** | PO total was blank → Genuity calculated 12 × $4,850 = **$58,200.00** | Automated math verification |
| **Material Grade Normalized** | "SA-240 TP304L" from 6 different documents → all normalized to canonical form | Consistent records across systems |
| **Unit Error Corrected** | Tensile 94,720 "MPa" was physically impossible → converted from PSI → **653.07 MPa** (within spec 485-690) | Prevented catastrophic data error |
| **Old Spec Superseded** | Spec Rev 1 automatically marked as superseded by Rev 2 | Only latest spec used for validation |
| **Duplicate Scan Detected** | Certificate scan #10 identified as content-identical to certificate #5 via SHA-256 hash | No double-counting |
| **Missing Hardness Reading** | 8 of 9 HRC readings visible → median **14.05 HRC** computed as **analytics-only** (never certified) | Statistical gap filled safely |

### 🔴 BLOCKED FOR HUMAN REVIEW: 7 exceptions (Genuity refused to guess)

| Exception | Priority | Why Genuity Blocked It | Assigned To |
|---|---|---|---|
| **Quantity Conflict: PO says 12, Invoice says 11** | 🔴 CRITICAL | Sources disagree — Genuity records authority order but does NOT pick one | Procurement Operations (4hr SLA) |
| **Boron Value Missing on MTR** | ⚠️ NORMAL | Ladle analysis says 0.0002% but domain policy doesn't allow auto-substitution | Quality Engineering (24hr SLA) |
| **Tensile Strength Missing on MTR** | 🔴 CRITICAL | Original certificate stamp was obscured — no direct evidence | Quality Engineering (4hr SLA) |
| **Inspector Signoff Missing** | ⚠️ NORMAL | Final inspection report not signed yet | Quality Engineering (24hr SLA) |
| **Hardness Median** | ℹ️ INFO | Computed value kept as analytics-only — never loaded operationally | Document Operations (72hr SLA) |

### 🔗 Complete Evidence Chain Built Automatically:

```
PO:LTTS-PO-2024-0847
  → PART:PN-304L-PLT-0750
    → BOM:BOM-HDS-304L-R2
      → SPEC:SPEC-SA240-304L (Rev 2)
        → CERT:NAS-893611
          → HEAT:AN4T
            → TEST:CHEM-AN4T (Cr ✅, Ni ✅, Mo ✅, Nb+Ta ✅)
            → TEST:MECH-AN4T (Tensile 653 MPa ✅ within 485-690)
```

### 🧪 Chemistry Validation Results (All PASS):

| Element | Actual Value | Spec Min | Spec Max | Result |
|---|---|---|---|---|
| Chromium (Cr) | **18.211%** | 18.00% | 20.00% | ✅ PASS |
| Nickel (Ni) | **8.078%** | 8.00% | — | ✅ PASS |
| Molybdenum (Mo) | **0.277%** | 0.00% | 0.75% | ✅ PASS |
| Ni + Co (derived) | **8.122%** | — | — | ✅ PASS |
| Nb + Ta (derived) | **0.007%** | 0.00% | 0.10% | ✅ PASS |
| **Tensile Strength** | **653.07 MPa** (recovered from 94,720 PSI) | 485 MPa | 690 MPa | ✅ PASS |

### 🛡️ Integrity & Audit:
- **21/21 provenance integrity checks: PASS**
- Every accepted field has a traceable evidence ID back to the source document
- Domain pack snapshot and SHA-256 manifest included for audit trail
- Operational release: **BLOCKED** (write-back to ERP/QMS not allowed until human review complete)

---

# 4. BUSINESS IMPACT & KPIs

## 4.1 Cost Comparison (Per Record / 12 pages)

| Approach | Review Cases | Cost Per Record | Cost Per Page |
|---|---|---|---|
| **A: OCR Only** (manual review everything) | 31 | **$34.89** | $2.91 |
| **B: OCR + Basic Rules** | 18 | **$20.27** | $1.69 |
| **C: OCR + Reconciliation** | 9 | **$10.14** | $0.85 |
| **D: Full-Page VLM** (send every page to AI) | 12 | **$13.55** | $1.13 |
| **E: Genuity Selective Routing** ⭐ | 6 | **$6.77** | $0.56 |

> **Genuity costs 49.5% less per verified field than a Full-Page VLM approach, and 80.6% less than pure OCR with manual review.**

## 4.2 Time Savings

| Manual Process Today | With Genuity |
|---|---|
| **45–90 minutes** per MTR packet (cross-checking 8-12 documents) | **< 1 second** automated processing + **only 6 focused review cases** for human |
| Quality Engineer reviews **every** field | Quality Engineer reviews **only exceptions** |
| No automatic evidence linking | Full evidence chain with SHA-256 audit trail |
| Errors caught days/weeks later (or not at all) | Errors caught **instantly** before data enters ERP |

## 4.3 Scaling Economics

| Annual Volume | Manual Cost (OCR Only) | Genuity Cost | **Annual Savings** |
|---|---|---|---|
| 100,000 pages | $290,775 | $56,402 | **$234,373** |
| 1,000,000 pages | $2,907,750 | $564,020 | **$2,343,730** |
| 10,000,000 pages | $29,077,500 | $5,640,200 | **$23,437,300** |

## 4.4 Break-Even Analysis

| Implementation Cost | Pages to Break Even vs Manual | Pages to Break Even vs Full-Page VLM |
|---|---|---|
| $50,000 | **21,334 pages** (~1-2 months for large EPC) | 88,479 pages |
| $100,000 | **42,668 pages** (~2-4 months) | 176,958 pages |
| $250,000 | **106,668 pages** (~6-12 months) | 442,394 pages |

---

# 5. WHERE GENUITY HELPS LTTS SPECIFICALLY

## 5.1 Immediate Use Cases

| LTTS Service Line | How Genuity Helps |
|---|---|
| **MTR Validation** | Exactly this demo — automate chemistry/mechanical cross-check against specs |
| **PO Processing (UTAS MRO)** | Cross-document PO-Invoice-BoM reconciliation with conflict detection |
| **Smart Tagging & Document Comparison** | Genuity's graph engine links all documents in a chain with evidence |
| **CoC Data Extraction** | CoC acts as the bridge between PO and MTR — Genuity automates this link |
| **Specification Doc Extraction** | Spec limits drive the chemistry/mechanical validation rules |
| **Engineering Drawing Extraction** | BoM and part number validation against drawings |

## 5.2 What Genuity Does NOT Do (Honest Limitations)

| Limitation | Explanation |
|---|---|
| ❌ Genuity is **not an OCR engine** | It works **after** your existing OCR (AWS Textract, Google Document AI, Azure Form Recognizer) |
| ❌ Genuity does **not certify compliance** | It produces evidence for humans to make the compliance decision |
| ❌ Synthetic fixture precision ≠ real accuracy | The 100% precision on this demo is on synthetic/fixture data — a real blind pilot is required |
| ❌ No probabilistic gap-filling | Genuity never invents data to look better — if a value is missing, it stays missing |

---

# 6. RECOMMENDED NEXT STEP

> **A 4-week paid blind pilot on 10,000 real LTTS MTR packets** where:
> 1. LTTS provides real OCR output from their existing extraction stack
> 2. Genuity processes it and generates the reconciled records
> 3. An independent LTTS QA team scores the results against manually validated truth data
> 4. We measure: critical-field precision, exception reduction, time savings, and cost per verified field

**Target KPIs for pilot success:**
- ≥ 99.5% critical-field precision on accepted fields
- ≥ 30% reduction in exception handling time
- ≥ 30% lower cost per verified field vs current process
- Zero silent conflicts or unsupported auto-accepts

---

# 7. HOW TO RUN THIS DEMO LIVE

All files are in the folder: `LTTS_MTR_VALIDATION_DEMO`

```powershell
# From the Genuity2.0 usecase1 directory:
$env:PYTHONPATH = "$PWD\source"

# Run Genuity on the LTTS demo packet:
py -3 -m genuity_reconcile run `
  --ocr-dir "..\LTTS_MTR_VALIDATION_DEMO\ocr_packet" `
  --output-dir "..\LTTS_MTR_VALIDATION_DEMO\genuity_output_live" `
  --domain-pack "..\LTTS_MTR_VALIDATION_DEMO\ltts_sa240_304l_domain_pack.json"
```

**Output files to show:**
- `SUMMARY.md` — One-page result summary
- `review_queue.json` — The 7 exceptions Genuity flagged
- `validation_report.json` — Chemistry/mechanical validation results
- `cost_report.json` — 5-scenario cost comparison
- `business_case.json` — Scaling economics and break-even
