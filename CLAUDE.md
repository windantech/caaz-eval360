# CAAZ Performance360 — Aviation Safety, Compliance & Performance Management System · CLAUDE.md

Last updated: 2026-10-06 (demonstration build 1.0)

A demonstration of **Eval360 configured for the Civil Aviation Authority of Zimbabwe (CAAZ)**. It
answers one question — *is Zimbabwe's civil aviation system operating safely, securely, efficiently
and in compliance with national and international requirements?* — by connecting ICAO requirement →
CAAZ regulation → oversight → inspection → finding → safety risk → corrective action → evidence →
verification → compliance → safety improvement.

Architecture and rules follow the KDC demonstration (`../kdc-eval360`), which follows CIC and FPC.
Same single-file pattern, same conventions.

**Eval360 is the performance, compliance, assurance, risk and management layer.** It does not
replace ATC, radar, flight planning, aeronautical information, aircraft registry, licensing or
operational surveillance systems (brief §107). Nothing in the demo may suggest otherwise.

---

## Two kinds of data — never mixed silently

| Provenance | What | How it is shown |
|---|---|---|
| `PUBLIC_CAAZ` | Facts published by CAAZ — functions, mandate, vision, mission, values, the 2026 priorities, regulatory domains, the SSP and SMS approach, the SARPs obligation, airworthiness/aerodrome/licensing functions, ANS structure, security forms, the two commissioned systems, ATAZ TRAINAIR PLUS Bronze, the air service agreements | Green **Public CAAZ Information** badge (`pubBadge(key)`); click opens the source |
| `DEMO_SYNTHETIC` | Every entity, aircraft, licence, inspection, finding, CAP, ICAO assessment, SPI value, occurrence, risk, asset reading, project score, course, complaint, action | Dashed **Illustrative Demo Data** badge (`demoBadge()`), tooltip "This record exists solely to demonstrate Eval360 functionality." |
| `CALCULATED` | Indices derived from the records (safety performance, ICAO compliance, CAP closure rate…) | `calcBadge()` |
| `USER_ENTERED` | Anything changed during a session | Audit trail with old value, new value and reason |

- Every public fact lives in `PUBLIC` and names a source in `SOURCES`. **All were checked against
  the source on 6 October 2026** and are `CONFIRMED`; where the brief paraphrased, the source wording
  is used. A consistency check fails if any public fact lacks a source or a confirmed status.
- Public and synthetic content sit in visibly separate zones (`.zone pub` / `.zone demo`).
- **No confidential aviation safety information is inferred.** No real operator is named in any
  synthetic record; entity names are fictional ("ZimAir Demo Ltd", "… Demo A"). Aircraft
  registrations are `Z-D001`…`Z-D172` — the digits make them impossible as real Zimbabwean marks.
- **There is no public ICAO USOAP effective-implementation score for Zimbabwe in the demo.** The
  86% ICAO figure is an illustrative internal self-assessment, and every screen that shows it says so.

### Source register (verified 6 Oct 2026)

| Key | Source | Supports |
|---|---|---|
| SRC-ABOUT | caaz.co.zw/about-us | Functions (s.3, Civil Aviation Amendment Act 2018), mandate, vision, mission, values, tagline, separation from airport operations |
| SRC-REG | caaz.co.zw/regulatory-services | Regulatory domains, SARPs obligation, five-phase AOC certification, consumer protection "under development" |
| SRC-AW / SRC-AD / SRC-PEL | Airworthiness · Aerodromes and Ground Aids · Personnel Licensing pages | Domain functions; SI 176 of 2019 |
| SRC-SMS | Safety Management Systems and Accident Investigation | State Safety Program purpose, SMS approach, mandatory and voluntary reporting |
| SRC-SEC | Aviation Security and Facilitation | A.S.18, A.S.7 (CAP form), A.S.10, A.S.9, A.S.8, A.S.4, A.S.39; SI 69 of 2022; annual programme review |
| SRC-ANS | Air Navigation Services | ANS structure (ATM, Aeronautical SAR, CNS, MET, AIM, PANS-OPS) |
| SRC-NY26 | DG New Year message, 9 Jan 2026 | The 2026 priorities under NDS2 |
| SRC-YE24 | DG year-end message, 31 Dec 2024 | SSR and ATC communications commissioned; ATAZ TRAINAIR PLUS Bronze; South Africa ASA (150/week → unlimited); new ASAs Kuwait, Rwanda, Chad; reviewed Malawi, Malaysia, The Gambia |

URLs are recorded in `SOURCES` and on the Master Data & Sources screen.

---

## Where this build departs from the brief, and why

| Brief | Built | Why |
|---|---|---|
| Safety trend Q1 2025 78% → Q2 2026 87% (§20) | Shifted one quarter: Q2 2025 78% → Q2 2026 86% → **Q3 2026 87%** (live) | Fixed clock is 6 Oct 2026; Q3 2026 has just closed and is the reporting period. The live point is the index, not a typed number |
| Eight 2026 priorities (§9) | Seven published priorities, tracked as **eight scored lines** — "improved safety and security oversight" split into its safety and security halves | The source lists seven; the split is labelled |
| "Safety Performance 87%" (§71, no definition) | Status-weighted index of the 25 SPIs: on target 100, needs attention 75, off target 25, critical 0 → 17 / 6 / 1 / 1 = **87.0** | Configurable on Settings; a plain average of achievements would hide the critical SPI-003 |
| "ICAO Compliance 86%" (§32) | 184 compliant ÷ 214 assessed = 86.0%, **internal self-assessment** | No published USOAP score was found; none is implied |
| "Strategic Performance 76%" (§71) | Weighted mean of the eight priority-line scores (75.6) | Weights on Settings |
| "ANS Availability 99.4%" | Mean availability of the eight CNS assets | Derived, not typed |
| CAP closure rate (SPI-004) 82% | CAPs that fell due in Q3 2026 and were closed by their due date: **41 of 50** | Derived from the CAP register |
| Aerodrome register (§44) | Five **fictional** aerodromes, operated by a fictional operator | CAAZ was separated from airport operations in 2018 (Airports Company of Zimbabwe); CAAZ regulates aerodromes |
| Year-end milestones (§50–§57, §64) | Dated **2024** (source dated 31 Dec 2024) | Source date |
| ATAZ TRAINAIR PLUS Bronze | Audited Nov 2024; award presented 12 Feb 2025 (noted) | Source |
| Functions, domain names | Source wording ("Aviation Security and Facilitation", "Aerodromes and Ground Aids", "Safety Management Systems and Accident Investigation") | Source |
| Directorates (§11) | Includes **Corporate Services** as a demo grouping of the published finance, corporate-secretariat and internal-audit functions | Labelled as a grouping |
| Public infrastructure projects (§50–§51) | Status public; **budget "not published"**; scores and benefits synthetic; start and commissioning dates illustrative but placed before 31 Dec 2024 | No public budget figures; the source already reports both as commissioned at that date |

All other quoted figures are derived from the records and asserted by the consistency checks —
including 67 open CAPs (18 high, 4 critical, 21 pending verification, 9 overdue, 43 closed in Q3),
CAP-2026-036, INS-2026-0173 (84%, 2 Major + 4 Minor, 6 CAPs), ICAO 214 / 184 / 21 / 9 with 30
findings (4 critical, 6 overdue, 3 due in 7 days) and ICAO-FSS-2026-014, SSP 41/50, the airworthiness,
security, ANS, training, complaints and management-action figures, SAF-2026-0048, and the §72 alerts.

---

## Layout, rules, testing

- `caaz_eval360_demo.html` is the source of truth; edit it directly. No build step, no framework.
- Fixed clock **6 Oct 2026**; calendar quarters. Reporting period Q3 2026, closes 15 Oct 2026.
- Every figure derived (section 18); quotas exact (`quota()`); generators are order-dependent —
  run the self-test after any change to section 15.
- All date arithmetic in UTC (`addDays`, `daysBetween`).
- No inline `onclick`; `data-action` + `ACTIONS` / `CHANGES` / `SUBMITS`.
- Roles, not people: fourteen role accounts (brief §10). Opens directly on the Executive
  Dashboard as the Director General; switch roles from the name in the top bar.
- CAP verification (§82): operator evidence → inspector accepts / asks for clarification / rejects
  (`canVerifyCap`). KPI submissions: submitted → reviewed by a director (`canReview`) → validated by
  the Safety Manager (`canValidate`).
- Audit trail (§83): `addLog(text, ref, icon, {old, new, reason})`.

```bash
bash scripts/selftest.sh     # every screen × 14 roles + data checks; exit 1 on failure
```

Open any screen directly: `caaz_eval360_demo.html#cap-detail/CAP-2026-036/insp`.

## Working agreement

1. Self-test before every commit.
2. A new public fact needs a `SOURCES` entry and a check against the source before it gets the
   Public badge. Until then it is synthetic.
3. If CAAZ supplies real oversight data, it replaces the synthetic records — and the provenance
   changes with it. Real safety data stays out of this public repository.
