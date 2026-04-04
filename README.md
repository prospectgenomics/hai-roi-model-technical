# HAI Prevention Value Calculator — Technical/Publication Tool

**Prospect Genomics** — Full decision-analytic model for peer review and publication

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
