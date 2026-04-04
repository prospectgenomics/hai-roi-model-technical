# Publication Plan: HAI Prevention Value Calculator
## Translating the Model into a Peer-Reviewed Manuscript

**Working title:** "Decision-Analytic Cost-Benefit Model of Whole-Genome Sequencing Surveillance Intensity in Hospital Infection Prevention: A Comparison with Conventional Epidemiology"

**Lead author:** Shawn Hawken, Prospect Genomics  
**Target journals (in priority order):** Infection Control & Hospital Epidemiology (ICHE/SHEA), Antimicrobial Stewardship & Healthcare Epidemiology (ASHE), Value in Health (ISPOR), OFID  
**Target conference:** SHEA Spring 2026, ID Week 2026  
**Estimated manuscript completion:** Q3 2026

---

## Phase 1 — Strengthen the Evidence Base (Now → 3 months)

These are the gaps most likely to draw reviewer criticism. Address before submission.

### 1.1 Detection rate validation
The per-model detection rates (M1=90%, M2=73%, M3=40%, M4=20%) are currently expert-derived.

**Action:** Conduct a systematic literature search (PubMed, Embase) for prospective WGS surveillance studies reporting:
- % of genomic clusters detected per surveillance intensity category
- Cluster size distribution (to validate avgCluster=5 assumption)
- Turnaround time distributions

**Target references to find or generate:**
- Any prospective RCT or quasi-experimental study comparing WGS detection rates across intensity levels
- If none exist, explicitly frame as expert-derived with uncertainty bounds and argue for face validity

### 1.2 Transmissible fraction validation
TRANS_FRAC values (CLABSI 45%, CAUTI 32%, CDI 38%, MRSA 42%, VAE 38%) are currently drawn from single-center WGS studies.

**Action:** Meta-analysis (informal or formal) of published WGS studies reporting the proportion of HAIs attributable to cross-transmission. Key citations already in model: R14, R15, R20. Expand search.

### 1.3 Conventional detection rate (comparator arm)
The conventional detection rate of 7% is the model's most novel and challenging assumption — reviewers will scrutinize this.

**Action:** Find 2–3 studies that directly compared genomically-defined transmission clusters to those identified by conventional epi alone. Bhargava 2021 (R13) and Shenoy 2024 (R20) are a start. Need a stronger citation base for 5–15% range.

---

## Phase 2 — Model Formalization (Months 2–4)

### 2.1 Structure the paper following CHEERS 2022

The app already implements CHEERS 2022 (R21) and ISPOR-SMDM 2012 (R22). The manuscript sections map as follows:

| CHEERS Item | Paper Section | Status |
|---|---|---|
| Title + Abstract | Health economic evaluation | Draft |
| Introduction | Why WGS surveillance, gap in evidence | Draft |
| Target population | NHSN-reporting acute care hospitals | Done |
| Setting & time horizon | Hospital, 1-year, US 2024$ | Done |
| Comparator | Conventional IPC, no typing | Done |
| Perspective | Hospital (institutional) | Done |
| Discount rate | None (1-year horizon) | Done |
| Outcomes | HAIs prevented, net value, ICER | Done |
| Measurement of effectiveness | detRate × TRANS_FRAC × pFrac × lag | Done (needs validation) |
| Resources and costs | AHRQ 2017, inflated to 2024 | Done |
| Currency, price date | 2024 USD, CPI Medical | Done |
| Characterization of uncertainty | PSA (12-parameter Monte Carlo) + tornado | Done |
| Heterogeneity | Hospital size subgroups (4 tiers) | Done |

### 2.2 Formalize the ICER presentation
The ICER (cost per additional HAI prevented vs. conventional epi) is the key decision-analytic output. In the paper:
- Report ICER for each model at each hospital size tier
- Compare against published WGS cost-effectiveness thresholds from the literature
- Note: there is no established "willingness-to-pay" threshold for HAI prevention in the US; frame as decision-maker input

### 2.3 QALY / mortality layer
The QALY calculation (HAI_MORTALITY × QALY_PER_DEATH=5) needs a stronger evidence basis for publication. Options:
- Use CDC estimates of HAI-attributable mortality with confidence intervals
- Reference the QALY loss per HAI type from published burden of illness studies
- If this layer is too uncertain, consider reporting it as a secondary outcome or sensitivity analysis only

---

## Phase 3 — External Validation / Collaboration (Months 3–6)

### 3.1 Academic collaborator
This model will receive substantially less reviewer skepticism with a non-commercial co-author from an academic medical center.

**Action:** Identify 1–2 hospital epidemiologists or health economists at academic medical centers who use WGS and might co-author. Ideal profile: ID/IP faculty who have published WGS outbreak investigations.

### 3.2 Hospital data validation
Apply the model to 1–2 real hospital datasets (de-identified) to test face validity. Key checks:
- Do modeled outputs match the hospital's known WGS experience?
- Are cluster sizes consistent with avgCluster=5?
- Does the HACRP savings estimate feel plausible to the IP team?

### 3.3 Expert advisory review
Before formal submission, share the pre-print or near-final draft with 2–3 hospital epidemiologists (e.g., SHEA members) for informal review. Pay attention to:
- Does the comparator (no typing) feel realistic?
- Is the pFrac range plausible?
- Is the HACRP model fair?

---

## Phase 4 — Manuscript Drafting (Months 4–6)

### Suggested outline

**Abstract** (~250 words): Background (HAI burden), objective (model WGS surveillance value vs. conventional epi), methods (decision-analytic CBA, hospital perspective, PSA), results (ICER by model and hospital size), conclusions.

**Introduction** (1 page):
- HAI burden and cost (cite R1–R6)
- WGS as emerging IP tool (R20, Shenoy 2024)
- Gap: no published CBA of WGS surveillance intensity across hospital sizes
- Objective: develop and validate a transparent, publicly available model

**Methods** (2–3 pages):
- Model structure (decision tree, static, 1-year)
- Population: 4 hospital size tiers benchmarked to NHSN
- Interventions: M1–M4 WGS intensity levels (define each)
- Comparator: conventional epi, no molecular typing (define explicitly)
- Outcomes: HAIs prevented, cost avoided, HACRP savings, net value, ICER
- Data inputs (table): all parameters with source, central estimate, PSA distribution
- PSA: 12-parameter Monte Carlo, 10K iterations, report mean ± 95% CrI, P(benefit>0)
- One-way sensitivity: tornado diagram (9 parameters)
- HACRP: continuous approximation of binary threshold — acknowledged limitation
- Software: React/JavaScript (open source, publicly available at [URL])

**Results** (2–3 pages):
- Base case: net annual value by model and hospital size (table)
- ICER table (cost per HAI prevented vs. conventional, by model × hospital size)
- PSA results: mean ± 95% CrI, P(net benefit > 0)
- Tornado: top 3 drivers of uncertainty
- Subgroup: hospital size effect on all outcomes
- QALY/cost-per-QALY as sensitivity

**Discussion** (1.5 pages):
- Main finding: WGS surveillance M1/M2 generate positive ROI at medium-large hospitals even under conservative assumptions
- Key uncertainty: detection rates (no prospective RCTs), transmissible fraction estimates
- Limitation of HACRP continuous modeling
- Limitation: no societal perspective, no NTM/Candida auris
- Comparator choice: conventional epi with no typing is the real-world baseline
- COI statement: model developed by WGS vendor; academic co-authors; code open source

**Conclusion**: Frame as a planning tool for hospital IP teams, not a financial guarantee.

**Tables:**
1. Parameter inputs with distributions (PSA ready)
2. Base case results by model × hospital size (net value, ICER)
3. PSA results (mean, 95% CrI, P(benefit>0)) by model

**Figures:**
1. Model structure diagram (decision tree schematic)
2. Tornado diagram (base case, M1, academic hospital)
3. Net value by hospital size and model (heatmap or bar chart)
4. PSA scatter or density plot (cost-effectiveness plane, if QALY layer is used)

---

## Phase 5 — Pre-print and Submission (Months 6–8)

### 5.1 Pre-print
Post to medRxiv before journal submission. This establishes priority, invites community feedback, and is standard in health economics.

### 5.2 COI and disclosure
- Shawn Hawken: employee and co-founder, Prospect Genomics (company sells the described service)
- All academic co-authors: no COI
- Funding: self-funded / Prospect Genomics
- Model code: open source (link to GitHub)

### 5.3 Data availability
- Model code: GitHub (already public)
- Input data: all from published sources (AHRQ, NHSN, CDC) — no private data
- No IRB required (no patient data)

---

## Key Methodological Vulnerabilities to Pre-empt in the Paper

| Vulnerability | Mitigation |
|---|---|
| Detection rates are expert-derived, not empirical | Report as assumptions with wide uncertainty bounds; PSA samples M1/M2 |
| pFrac (cluster interruption) has no RCT validation | Cite Toth 2022 indirect evidence; PSA samples around user value; frame as conservative vs. optimistic |
| HACRP is modeled continuously | Explicitly acknowledge binary threshold limitation; present as directional, not precise |
| COI: we sell this service | Co-author from academic center; open source code; CHEERS disclosure; PSA shows uncertainty |
| Conventional epi baseline detection rate (7%) | Cite WGS comparison studies; present range 3–15% in tornado |
| M4 reservoir ID rate (55%) | Cite Bhargava 2021 directly; present 30–75% in tornado |

---

## Quick Reference: Key Numbers for Abstract/Results

*(Medium hospital, base case, subscription $100K/yr, pFrac=75%)*

| Model | HAIs prevented/yr | Net value (sub) | ICER vs. conv. |
|---|---|---|---|
| M1 Full Surveillance | ~11 | +$480K | ~$9K/HAI |
| M2 Prospective | ~8 | +$330K | ~$12K/HAI |
| M3 Semi-Prospective | ~4 | +$80K | ~$26K/HAI |
| M4 Retrospective | ~1 | −$60K | N/A |

*Numbers are illustrative — pull from live model before submitting.*

---

## Contacts / Resources

- SHEA abstract submission: typically opens August for spring conference
- ID Week abstract: typically opens March for October conference
- ICHE editor: currently Dr. Silvia Munoz-Price
- Value in Health: uses ScholarOne; requires structured abstract with outcomes framing
- medRxiv: free, no review, posts within 24h
