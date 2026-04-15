# HAI Prevention Value Calculator — Technical/Publication Tool

**Prospect Genomics** — Full decision-analytic model for peer review and publication

**Live app:** https://prospectgenomics.github.io/hai-roi-model-technical/

**Private repository** — not for public distribution prior to manuscript submission.

---

## What this is

A rigorous decision-analytic cost-benefit model comparing four levels of whole-genome sequencing (WGS) surveillance against a conventional epidemiology baseline (no molecular typing) in hospital infection prevention. Built to support peer-reviewed publication following CHEERS 2022 and ISPOR-SMDM 2012 standards.

The simplified sales-facing version of this tool lives at: `prospectgenomics/hai-roi-model` (public).

---

## Features

- **Conventional epi comparator** — explicit baseline arm (no typing, 7% detection rate, 8-case lag)
- **ICER** — incremental cost per HAI prevented vs. conventional baseline, per model and hospital size
- **Probabilistic Sensitivity Analysis (PSA)** — 12-parameter Monte Carlo (1K/5K/10K iterations), reporting mean ± 95% credible interval and P(net benefit > 0)
- **Tornado diagram** — one-way sensitivity across 9 parameters, sorted by impact
- **QALY layer** — optional toggle for cost per QALY, using HAI-attributable mortality rates
- **Advanced parameters** — all hardcoded assumptions exposed and adjustable (detection rates, avg cluster size, HACRP exposure fraction, M4 reservoir ID rate, conventional detection rate)
- **28 peer-reviewed references** with clickable navigation to full citations
- **All assumptions documented** with confidence ratings and PSA distributions

---

## Tabs

| Tab | Description |
|---|---|
| Overview | 4 model cards with ICER, net value, incremental HAIs prevented |
| HAI Breakdown | Per-infection-type prevention table + HACRP penalty exposure |
| Sub vs. Ad Hoc | Pricing comparison, crossover analysis |
| PSA & Sensitivity | Monte Carlo results + tornado diagram |
| Documentation | Assumptions, methods, formula, all 28 references |

---

## Controls & parameters reference

| Control | Default | Range | What it does |
|---|---|---|---|
| **Benchmark Hospital** | Medium | Small / Medium / Large / Academic | Pre-filled profiles from NHSN national HAI rates, HCUP volume data, and Definitive Healthcare revenue benchmarks |
| **Total Revenue ($M)** | $175M | Any | Sets the Medicare revenue base for HACRP penalty calculation |
| **Medicare Revenue %** | 23% | 10–45% | Fraction of revenue from Medicare FFS — scales the max 1% HACRP penalty |
| **HAI Counts** | Benchmark | Any | Annual NHSN-reported events by type. Drives the prevention calculation directly. |
| **Culture Volumes** | Benchmark | Any | Annual positive cultures by organism. Determines sequences/yr and ad hoc program cost. |
| **Cluster Interruption Rate (pFrac)** | 75% | 0–100% | % of WGS-identified clusters that IP successfully interrupts. Core efficacy assumption. Literature: 47–85% (Toth 2022). |
| **Sequencing TAT** | 3 days | 12 hr – 3 mo | Turnaround time from sample to result. Affects M1 and M2 only — longer TAT increases intervention lag. |
| **Annual Subscription Fee** | $100K/yr | $25K–$300K | Flat program cost for subscription pricing model |
| **Ad Hoc Price / Sample** | $300 | $175–$500 | Per-genome price for pay-per-use model. Floor $175 = ~50% margin. |
| **SSI toggle** | Off | On/Off | Includes surgical site infections in HAI counts and culture volumes |
| **QALY layer toggle** | Off | On/Off | Shows cost per QALY on model cards using HAI mortality rates × 5 QALYs/death |
| **Cost Perspective** | Total | Total / Variable | Total = full attributable HAI cost. Variable = avoidable ~65% (Graves 2007) — preferred for hospital budgeting. |
| **Conventional Detection Rate** *(Advanced)* | 7% | 1–20% | % of genomic clusters detectable by conventional epi with no typing. PSA SE = 3%. |
| **Avg Cluster Size** *(Advanced)* | 5 cases | 2–12 | Average transmission cluster size before intervention. Scales the lag fraction. |
| **M4 Reservoir ID Rate** *(Advanced)* | 55% | 10–90% | M4 only: % of retrospective outbreaks where WGS identifies a persistent reservoir (Bhargava 2021). |
| **HACRP Baseline Exposure** *(Advanced)* | 40% | 10–80% | Fraction of max Medicare penalty the hospital is currently exposed to. Continuous approximation of binary CMS threshold. |
| **Detection Rates M1–M4** *(Advanced)* | 90/73/40/20% | 5–100% | Fraction of true genomic clusters each model detects. Expert-derived; M1/M2 sampled in PSA. |

---

## Running locally

```bash
npm install
npm start
```

Build for deployment:
```bash
npm run build
```

---

## Key methodology

- **Comparator:** Conventional IPC (clinical epi + manual contact tracing, no molecular typing). Cost = $0 incremental. Detection rate = 7% (PSA SE = 3%). Intervention lag = 8 cases.
- **Cost basis:** AHRQ 2017 meta-analysis (hospital perspective, 2015 USD), inflated +29% to 2024 via CPI Medical Care Services
- **Variable cost fraction:** 0.65 of total (Graves 2007) — toggle between variable and total
- **Intervention lag:** lagFrac = min(interventionLagCases × TATscale / avgCluster, 0.85)
- **M4 formula:** annual × TRANS_FRAC × pFrac × reservoirRate × (avgCluster / annual)
- **HACRP:** Continuous approximation of binary CMS threshold — acknowledged limitation
- **Reporting standard:** CHEERS 2022, ISPOR-SMDM 2012

---

## Publication plan

See `PUBLICATION_PLAN.md` for the full manuscript strategy, target journals, timeline, and gap analysis.

---

## Conflict of interest

Developed by Prospect Genomics. Authors are employees of the company selling the described service. Code is open-sourceable at time of manuscript submission. All methods and assumptions are fully documented and exposed for scrutiny.

---

*© Prospect Genomics · [prospectgenomics.bio](https://prospectgenomics.bio) · shawn@prospectgenomics.bio*
