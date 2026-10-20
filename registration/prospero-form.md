# PROSPERO 注册填报表

> 项目：`melatonin-sleep-perf`　起草：2026-10-19　字段数：40（必填 26）

## ★ 只能由登记者本人做的两项

- **字段 5（Stage of review at time of this submission）** — 阶段勾选（Started / Completed 两组复选框）+ 可选补充说明。 这是登记者本人的声明项：PROSPERO 条款写明「Reviews must be registered before data extraction has started」，且「Action will be taken if inaccuracies ... including information supplied about the stage of review ... Deliberate falsification 视为 research misconduct」。本文件不代填，也不为该项提供脚本值。
- **字段 38（Current review status）** — Current review status。必须与字段 5 的勾选自洽；勾选后不可编辑。

## 一致性检查

- `include_timing_note = false` —— 字段 39 **不含**回顾性说明。若字段 5 按前瞻性勾选，而稿件与偏差记录（SAP §10）显示提取已完成，两者之间存在可被抽查的缺口。此项由登记者裁定。
- 字段 5 与 38 必须互相自洽；PROSPERO 在勾选后不允许编辑这两项。

## 字段正文（按 1→40 顺序）

### 1. Review title *

```text
Oral melatonin supplementation and sleep, exercise performance, oxidative stress
and inflammation in exercising populations: a systematic review and meta-analysis
```

### 2. Original language title

```text
口服褪黑素补充对运动人群睡眠、运动表现、氧化应激与炎症的影响：系统综述与 Meta 分析
```

### 3. Anticipated or actual start date *

```text
17 October 2026.
(Date on which the eligibility criteria and the analysis plan were complete and the
formal screening of identified records began.)
```

### 4. Anticipated completion date *

```text
31 December 2026.
```

### 5. Stage of review at time of this submission *

> **人工操作**，阶段勾选（Started / Completed 两组复选框）+ 可选补充说明。 这是登记者本人的声明项：PROSPERO 条款写明「Reviews must be registered before data extraction has started」，且「Action will be taken if inaccuracies ... including information supplied about the stage of review ... Deliberate falsification 视为 research misconduct」。本文件不代填，也不为该项提供脚本值。

### 6. Named contact *

```text
Tianyuan He
```

### 7. Named contact email *

```text
danielho3062566618@gmail.com
```

### 8. Named contact address

```text
Guangzhou Sport University, Guangzhou, Guangdong, China
```

### 9. Named contact phone number

> 有意留空 —— 联系电话非必填，留空（PROSPERO 会把字段 8 地址公开，故地址也只填机构层级）。

### 10. Organisational affiliation of the review *

```text
Guangzhou Sport University, Guangzhou, Guangdong, China.
The review is unfunded and has no sponsor.
```

### 11. Review team members and their organisational affiliations *

```text
Tianyuan He — Guangzhou Sport University, Guangzhou, Guangdong, China.
Sole member of the review team; responsible for the search strategy, eligibility
criteria, screening, data extraction, statistical analysis and write-up.
No second independent screener or extractor took part; this is stated as a
limitation rather than presented as duplicate independent work.
```

### 12. Funding sources/sponsors *

```text
None. This review received no funding from any agency, foundation or commercial
entity. Computing resources were personal equipment.
```

### 13. Conflicts of interest *

```text
None declared. The author has no financial relationship with any manufacturer,
distributor or agent of melatonin or sports-nutrition supplements, and has
received no payment, gift or funding from that industry. Use of AI tools is
disclosed in item 39.
```

### 14. Collaborators

```text
None.
```

### 15. Review question *

```text
In exercising populations, what is the effect of oral melatonin supplementation,
compared with placebo or no treatment (or within-subject control), on four outcome
domains: (1) sleep, (2) exercise performance, (3) oxidative stress and
(4) inflammation?

Secondary questions: does the effect vary with dose (continuous meta-regression on
dose in mg); does it vary with comorbidity status, study design (parallel vs
crossover) or timing (acute vs >= 1 week); and what are the risks of bias and the
certainty of the evidence?

The review issues no clinical recommendation. Certainty of evidence is rated with
GRADE and stops there; no strength-of-recommendation judgement is made.
```

### 16. Searches *

```text
Bibliographic databases:
- PubMed (NCBI E-utilities): 379 records, searched 17 October 2026.
- Web of Science Core Collection: 56 records, searched 17 October 2026.
- Scopus: 46 records, searched 17 October 2026.
- CNKI (China National Knowledge Infrastructure): 5 records, searched 17 October 2026.
Total: 486 records.

Citation tracking (forward and backward), run on the same corpus: Lens.org 427 citing and 1070 cited records; OpenAlex / COCI / Europe PMC 762 citing and 2029 cited records; union after de-duplication 1189 citing and 3099 cited records. Citation-tracking records were screened together with the database records.

No language limit and no date limit were applied at the search stage (records were screened for language afterwards). The search strings were designed so that the design block is a free-text randomisation block rather than a publication-type filter, because the index tag under-covers recent records; sensitivity was preferred at the search stage and specificity at the screening stage.

No trial-registry search, no grey-literature search, no hand searching of reference lists beyond the citation-tracking channels above, and no contact with authors.
```

### 17. URL to search strategy

```text
The full search strings for all four databases are released with the review
(file `queries.yaml`, published alongside the manuscript). No separately hosted
URL at the time of registration.
```

### 18. Condition or domain being studied *

```text
Exercise and sport. Four outcome domains are studied:
(1) sleep — quality and architecture (sleep efficiency, latency, total sleep time,
wake after sleep onset); (2) exercise performance — aerobic capacity, strength,
power, sprint and agility time, time to exhaustion; (3) oxidative stress — MDA,
AOPP, SOD, CAT, GPx, TAC, GSH, FRAP; (4) inflammation — CRP, IL-6, TNF-alpha,
IL-10, CK, LDH.
```

### 19. Participants/population *

```text
Exercising populations: athletes, regular exercisers and people with a training
background, identified from reported participant characteristics (sport, competitive
level, years of training or weekly training volume). No threshold on training
frequency or duration is applied and no age restriction is applied; children and
adolescents, and older adults, are recorded as stratification variables.

Main (strict) analysis: exercising populations without comorbidity.
Sensitivity analysis: populations with comorbidity who perform exercise
(for example dialysis, obesity, multiple sclerosis, autism spectrum disorder),
with all other criteria unchanged.

Insomnia symptoms are a stratification variable, not an eligibility condition.
```

### 20. Intervention(s), exposure(s) *

```text
Oral melatonin supplementation, any dose (2-100 mg in the identified literature) and
any duration. Single acute doses are eligible.

Excluded: topical or injected melatonin; melatonin-receptor agonists (ramelteon,
agomelatine and similar) used alone.
```

### 21. Comparator(s)/control *

```text
Placebo, no treatment, usual care, or the within-subject control condition of a
crossover trial.
```

### 22. Types of study to be included *

```text
Randomised controlled trials, parallel-group or crossover. Verifiable randomisation
is required: the report must describe a group-allocation method or use terms such as
random, randomly or randomised. Trials described only as double-blind, with no basis
for randomisation, are excluded.

Excluded publication types: animal and in-vitro studies, reviews and meta-analyses,
conference abstracts, study protocols without results, and retracted studies.
```

### 23. Context

```text
Supplementation of exercising populations in training or competition settings. Sleep
studies were conducted in the laboratory or at home. Populations with comorbidity who
perform exercise are handled in a separate sensitivity analysis rather than mixed
into the main analysis.
```

### 24. Main outcome(s) *

```text
Four outcome domains, pooled separately at domain level:
(1) sleep; (2) exercise performance; (3) oxidative stress; (4) inflammation.

Effect measure: Hedges' g (standardised mean difference), oriented so that a positive
value always favours melatonin.

Main time point, pre-specified: for acute studies, the measurement closest to exercise
completion (<= 60 min); for studies of >= 1 week, the post-intervention value at the
final measurement; for sleep studies, the night designated as primary by the report,
or the last night if unspecified.

No outcome domain is required to be present for inclusion.
```

### 25. Additional outcome(s) *

```text
Adverse events and dropouts attributed to supplementation, reported narratively.
Individual constructs within a domain are reported descriptively where pooling is not
defensible (for example oxidative-stress markers reported in non-comparable units).
```

### 26. Data extraction (selection and coding) *

```text
Extraction: each report is converted from PDF to Markdown and JSON (MinerU), then
structured into one YAML file per study, harmonised, and used to compute effect sizes.

Fields extracted: study identity, list of reports, cohort, DOI, title, year, journal,
design, randomisation statement, population, intervention, comparator, outcomes,
adverse events, language, funding, registration number, notes, effect sizes.

Extraction was performed by a single extractor (the author), with AI assistance for
reading values off figures. No independent duplicate extraction was performed.

Every effect size carries a source reference that resolves to the cell of the original
report (for example `Table 4!r12c3`); all effect sizes were re-read against the source
and every discrepancy was adjudicated against the source text. Where a report states
values only in a figure, values were read with the open-source `digitize` tool; error
bars read from figures were not used for variance estimation.
```

### 27. Risk of bias (quality) assessment *

```text
Risk of bias: RoB 2 for parallel-group trials and the RoB 2 crossover variant,
including the period-and-carryover-effects domain, for crossover trials.

Two assessment rounds were performed independently — one by an independent AI assessor,
one by the author — and disagreements were resolved by a documented adjudication
procedure. Agreement between rounds: weighted kappa 0.730.

Publication bias: funnel plots and Egger's test only where k >= 10. Three domains meet
this threshold; the sleep domain (k = 7) is reported as not assessed rather than as
free of bias.

No formal assessment of other sources of bias was performed.
```

### 28. Strategy for data synthesis *

```text
Random-effects meta-analysis with the REML estimator and the Hartung-Knapp-Sidik-Jonkman
adjustment (test = "knha"). Each domain reports the pooled SMD, its 95% confidence
interval, a 95% prediction interval, tau-squared, I-squared, Q, the number of studies
and the number of comparisons.

Effect size: Hedges' g with the average-variance standardiser (d_av), so that crossover
and parallel trials share one denominator —
d = (mean_MEL - mean_PLA) / sd_pooled, with
sd_pooled = sqrt((sd_MEL^2 + sd_PLA^2) / 2).

Design-specific variance:
- Parallel: vi = sd_pooled^2 * (1/n_MEL + 1/n_PLA), with small-sample correction.
- Crossover or within-subject: sd_diff = sqrt(sd_MEL^2 + sd_PLA^2 - 2 * r * sd_MEL * sd_PLA),
  vi = sd_diff^2 / n.

Within-condition correlation r was obtained in this order: (1) solved directly from
paired t/F statistics or a paired confidence interval reported for the same study and
outcome; (2) the median r of studies in this review that report paired statistics;
(3) the default r = 0.5, which is never applied silently — every row records its own
r_source. Sensitivity analyses use r = 0.2 and r = 0.8.

One comparison per study per domain is carried into the main analysis, so that studies
remain independent.

Input handling: median with interquartile range is converted with
sigma = IQR width / 1.349 and enters domain-level pooling only, never a single-outcome
pool. A missing standard deviation is substituted by the coefficient of variation of
comparable rows, never by an absolute standard deviation from another study.

Software: R with metafor for pooling and meta-regression; Python (pandas/numpy) for
the effect-size and contrast layer; an independent Python (numpy/scipy) implementation
reproduces the pooled results and is compared cell by cell.
```

### 29. Analysis of subgroups or subsets *

```text
Pre-specified subgroup analyses, exploratory only:
(1) comorbidity present vs absent (the primary subgroup);
(2) main vs sensitivity track;
(3) parallel vs crossover design;
(4) acute vs >= 1 week;
(5) dose as a continuous meta-regression on dose in mg and on log-dose, rather than
in dose bands — the only pharmacologically defined threshold, 0.5 mg, lies below the
lowest dose in this literature, and commercial dose bands are not pharmacodynamic
breakpoints.

Subgroup and meta-regression results are stated as conclusions only when k >= 10;
below that they are labelled exploratory. Between-group tests use the F statistic
reported under the knha adjustment. Leave-one-out leverage diagnostics are reported
for each meta-regression.
```

### 30. Type and method of review *

```text
Intervention review; systematic review with meta-analysis; quantitative synthesis of
randomised controlled trials. Not a diagnostic, prognostic, qualitative, or
methodological review.
```

### 31. Language

```text
English.
```

### 32. Country *

```text
China
```

### 33. Other registration details

```text
No other registration exists for this review, in PROSPERO or in any other registry.
```

### 34. Reference and/or URL for published protocol

```text
Not published separately. The statistical analysis plan (v1.0) and the eligibility
criteria are released with the manuscript and are available to the PROSPERO team on
request.
```

### 35. Dissemination plans

```text
Submission to a peer-reviewed journal. The registration materials and the statistical
analysis plan, with its dated deviation log, are deposited at https://github.com/DanielHo01/melatonin-sleep-perf-sr .
The analysis code, the structured extraction data and the harmonised effect-size table
are available from the named contact on reasonable request.

Not released: the full texts of included reports (publisher copyright) and the raw
screening decision table with its manual override patches. These are available from the
named contact for the purpose of reproducing the screening judgements, with
third-party copyright material removed.
```

### 36. Keywords

```text
melatonin; exercise; athletes; sleep; oxidative stress; inflammation; meta-analysis
```

### 37. Details of any existing review of the same topic by the same authors

```text
One registered review by the same guarantor addresses a related question:
CRD420261480362, an umbrella review of published systematic reviews and meta-analyses
on melatonin supplementation in athletes. It differs in unit of analysis. It summarises
published reviews, whereas this review re-derives effect sizes from the original
randomised controlled trials, and adds a continuous dose-response meta-regression.
No data extraction is duplicated between the two. Five further registrations by other
teams each address a single outcome domain; none pools the four domains in one model.
```

### 38. Current review status *

> **人工操作**，Current review status。必须与字段 5 的勾选自洽；勾选后不可编辑。

### 39. Any additional information

```text
AI tool disclosure.

Title and abstract screening: a deterministic rule engine, single assessor; every
decision was reviewed by hand and changed by the author where needed, with each change
recorded as a replayable patch. No language model took part in producing screening
decisions; a three-model vote with Fleiss' kappa was used only to calibrate the
screener's accuracy.

Full-text screening: manual, single assessor.

Data extraction: AI assistance for reading values off figures and from tables; every
extracted value was checked against the original report.

Risk of bias and certainty of evidence (GRADE): two independent rounds, one by an
independent AI assessor and one by the author, followed by documented adjudication.
Agreement between rounds is reported.

Code and documentation: AI-assisted drafting, reviewed, run and verified by the author.

AI tools did not make final inclusion decisions and were never the sole assessor of
risk of bias or of certainty of evidence.
```

### 40. Details of final report/publication(s)

```text
Not yet published. A manuscript is in preparation and will be submitted to a
peer-reviewed journal; this record will be updated with the citation once the review
is published.
```
