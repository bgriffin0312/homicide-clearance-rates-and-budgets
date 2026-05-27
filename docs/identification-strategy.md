# Identification Strategy for the Texas Homicide Clearance Project: Methodological Audit and TX Shock Scouting

Prepared for Brennan Griffin, May 2026.
Companion to `docs/literature-review.md` (May 2026) and `docs/case-level-approach.md` (May 2026). Read those first.

Scope: (1) audit whether the causal-inference papers already cited in this project's literature review are methodologically credible by 2026 standards — i.e., do they engage Goodman-Bacon (2021), Callaway-Sant'Anna (2021), Sun-Abraham (2021), de Chaisemartin-D'Haultfœuille (2020), Borusyak-Jaravel-Spiess (2024), Wooldridge (2021/2023), and Roth-Sant'Anna-Bilinski-Poe (2023); (2) scout Texas-specific shocks to detective staffing that could anchor a credible identification strategy; (3) recommend a primary design and one robustness design with a pre-analysis-plan sketch.

---

## TL;DR

- The existing causal literature on police resources and clearance is **pre-revolution by 2026 standards.** Bjerk (2022), the cleanest paper in the space, uses panel OLS with city and year fixed effects plus a 2SLS with lagged budget instruments — it does not engage Goodman-Bacon or the heterogeneous-treatment-effects literature at all. Mello (2019) is the modal exception: it is a single-shock 2009 ARRA-COPS RD plus a difference-in-differences with one treatment cohort, so the staggered-DiD critique does not bite. Evans & Owens (2007) is legacy TWFE and would not survive a modern re-estimation cleanly. The bar to clear is therefore low — even a careful CS-DiD or imputation event-study on TX data would be a meaningful methodological contribution.
- The single highest-credibility TX shock is **HB 1900 (87th Lege, 2021) plus SB 23 (87th Lege, 2021)** — the "defunding penalty" laws. They create a sharp **population-250,000 discontinuity**: 11 TX cities are bound by them, hundreds of TX cities just below the cutoff are not. That is an honest regression-discontinuity design on detective-budget stickiness, and to my knowledge it is unused in the academic literature.
- The runner-up is the **Houston PD 2021-2022 homicide-division expansion** (the canonical synthetic-control candidate the prior memo already flagged), now strengthened by the fact that we have actual reporting — 20 property-crime detectives transferred to homicide in March 2021, six additional cadet classes — that lets us date the shock cleanly to FY2021.
- The recommended **primary design** is a population-threshold regression-discontinuity using HB 1900/SB 23 as a force-of-law treatment on detective bureau headcount and clearance, with TX cities within ±25% of the 250K cutoff as the comparison set, and a **robustness synthetic control on Houston 2021-2022** as the within-state corroboration.
- The biggest threats to identification are: (a) HB 1900's penalty is so politically salient it generates anticipation effects and behavioral compliance in cities below the threshold that voluntarily lock in police budgets (selection on the running variable); (b) detective staffing as a treatment variable may not respond mechanically to HB 1900 even though aggregate police budget does (first-stage weakness); (c) clearance is measured with the reporting-convention problems documented in `docs/literature-review.md` — the case-level PIA pull described in `docs/case-level-approach.md` is the only way to get a defensible dependent variable.
- A pre-analysis plan must commit to (i) the exact RD bandwidth and donut specification before pulling case-level data, (ii) the case-level disposition outcome rather than agency-reported clearance, (iii) a falsification test on exceptional-clearance share, and (iv) explicit Roth-Sant'Anna honest pre-trends bounds rather than naive event-study graphs.

---

## 1. Methodological audit of the cited causal-inference literature

The table below covers every paper in `docs/literature-review.md` that purports to causally estimate the effect of police resources on crime or clearance, plus a handful of additional papers identified during this audit. "Modern-DiD-aware" means the published version engages at least one of Goodman-Bacon (2021), Callaway-Sant'Anna (2021), Sun-Abraham (2021), de Chaisemartin-D'Haultfœuille (2020), Borusyak-Jaravel-Spiess (2024), Wooldridge (2021/2023), or Roth et al. (2023) — or, if older, would not be vulnerable to those critiques given its design.

| Paper | Outcome | Estimator (published) | Modern-DiD-aware? | Likely fragility under CS/BJS re-estimation |
|---|---|---|---|---|
| **Bjerk (2022)**, *JELS* 19(3): 528-559 | Homicide clearance | Panel OLS with city + year FE; probit robustness for binary outcome; 2SLS with lagged-budget and state-revenue-shock instruments | **No.** Pre-dates and does not cite Goodman-Bacon. Identifying variation is within-city year-to-year budget changes, not a discrete shock. | Likely *robust* in direction, because the headline is a *null*. CS/BJS re-estimation of a null typically returns a noisier null — sign-flipping is unusual when the original is zero. But the standard errors are not credible by 2026 standards and the IV exclusion restriction (state revenue shocks affect clearance *only* through police budget) is heroic. |
| **Mello (2019)**, *JPubE* 172: 174-200 | Crime (not clearance) | **(a)** Regression discontinuity on the 2009 ARRA-COPS application-score cutoff (cleanest specification); **(b)** Difference-in-differences comparing 2009 grant recipients to non-recipients in pre/post-2009 design. Treatment is a single 2009 shock, not staggered. | **Partially.** Mello is a single-cohort DiD, so Goodman-Bacon's staggered-timing critique does not apply. The RD is the cleanest piece. He does not cite CS or BJS, but he wouldn't need to. | Findings should survive — a single-cohort DiD is mathematically equivalent to a 2x2 DiD and not subject to the Goodman-Bacon weighting problem. The RD is the credible piece and is robust to modern critiques because RD identification is orthogonal to the TWFE issues. |
| **Evans & Owens (2007)**, *JPubE* 91: 181-201 | Crime | Difference-in-differences comparing trends in crime before/after COPS grants in larger-vs-smaller-grant areas. Multiple grant cohorts (1994-2001) → **staggered treatment.** TWFE estimator. | **No.** Pre-dates the entire literature. | **Most fragile paper in the table.** Multiple grant waves (1995, 1996, 1997, etc.), all of which TWFE-pools together with later-treated and never-treated controls. The Goodman-Bacon decomposition would almost certainly produce forbidden comparisons. The elasticities of -0.26 (property) and -0.99 (violent) should be treated as suggestive, not definitive. Chalfin-McCrary's elasticity of -0.34 for violent crime (using a different identification) is the more reliable anchor. |
| **Chalfin & McCrary (2018)**, *REStat* 100(1): 167-186 | Crime | Panel IV using *measurement-error* correction in police hiring data as the identifying variation — not a DiD at all. Standard panel FE. | **N/A** (not a DiD design). | Robust. The identification doesn't depend on staggered-treatment-effect assumptions, so the modern DiD critique sidesteps it. |
| **Chalfin, Hansen, Weisburst & Williams (2022)**, *AER: Insights* | Crime, arrests | Panel IV exploiting variation in police hires from COPS grants and city-specific demand for officers; standard panel FE. | **N/A** (not a DiD design). Pre-print circulated in 2020; published 2022 just as the modern-DiD critiques peaked. | Robust to the staggered-DiD critique. The headline (0.1 fewer homicides per added officer) is the most-cited modern police-staffing-and-crime estimate. |
| **Weisburst (2019)**, *JPAM*, school police | Student outcomes | DiD exploiting variation in federal COPS school-police grants. Staggered treatment timing across districts. | **No.** Published just before Goodman-Bacon hit. | Findings on a *staggered* design from this period should be regarded as preliminary; Sun-Abraham or CS re-estimation would be a productive replication exercise. Not directly load-bearing for our clearance question, but cited because Weisburst is a respected name in policing econ. |
| **Weisburst (2024)**, *JHR* 59(4): 1122-1149, individual officers | Arrests | Movers design / individual-officer fixed effects, not a DiD at all. Treatment is officer-level "propensity," identified off random assignment to 911 calls. | **N/A** (not a DiD design). | Robust. The within-officer / between-officer decomposition is methodologically conservative. |
| **Braga & Dusseault (2018)**, *C&D* 64(3): 283-315 | Boston homicide clearance | Quasi-experimental ITS: Boston 2007-2011 pre vs. 2012-2014 post; compared against Massachusetts and U.S. agency trends. Single-shock, single-city. | **No engagement, but doesn't need to.** Single-shock ITS is not subject to the staggered-DiD critique. The valid concern is the parallel-trends assumption against the comparison series, not negative weights. | Robust to the modern-DiD critique. But the comparison-series choice is judgment-based, and Roth-Sant'Anna-style honest pre-trends bounds were never computed. A 2026-vintage replication would tighten the credibility. |
| **Braga, Turchan & Barao (2019)**, *JQC* 35(2): 285-318 | Boston homicide clearance | Logistic regression on case-level data with investigative-action predictors; controls for case mix; no DiD. | **N/A** (not a DiD design). | Robust. Effectively a case-mix-adjusted association study, not a causal identification of staffing's effect. |
| **Cook, Braga, Turchan & Barao (2019)**, *C&PP* 18(3): 525-551 | Boston clearance, gun homicides vs. assaults | Within-case survival analysis comparing homicide vs. nonfatal-shooting clearance trajectories. Not a DiD. | **N/A** (not a DiD design). | Robust. The identifying variation is "after 48 hours, effort diverges" — internal comparison, not cross-jurisdictional. |
| **Hsu, Emerick & Sytsma (2024)**, *Policing* 47(5): 786-803 | Clearance | Random-effects regression on 100-city panel 2000-2013; no shock-based identification, no DiD. | **N/A**, but the paper is observational. | Not subject to the DiD critique, but also not causal. Should be treated as descriptive. |
| **Hogan (2022)**, *C&PP* 21(3), Philadelphia de-prosecution | Homicide rate | Synthetic control (Abadie-Diamond-Hainmueller). | **N/A** (SCM, not DiD). | Robust to the staggered-DiD critique. SCM has its own credibility concerns (donor-pool sensitivity, placebo distribution), but those are different concerns. |

**Summary of the audit.** Of the eight identified "causal-inference" papers most load-bearing for this project, only two — Mello (2019) and Hogan (2022) — use designs that are intrinsically immune to the staggered-DiD critique (single-cohort DiD and SCM, respectively). Evans-Owens (2007) is the most vulnerable; it is also old enough that it has been largely superseded in citation practice by Chalfin-McCrary and Mello. **Bjerk (2022), the paper Brennan needs to beat, uses a panel-FE-plus-IV design that does not engage the modern DiD literature but is also not a true staggered-DiD design.** Its identification rests on the IV exclusion restriction (state revenue shocks affect clearance only through police budget), which is the more vulnerable assumption. A well-identified TX project does not need to outmaneuver Bjerk on the staggered-DiD axis; it needs to provide a more credible *source of exogenous variation* in detective staffing specifically.

## 2. The single best causal-inference paper currently in this literature

**Mello (2019), "More COPS, Less Crime," *Journal of Public Economics* 172: 174-200.** This is the bar to clear. The paper exploits the 2009 ARRA-COPS funding-score discontinuity: applications were scored 15-100, and DOJ awarded grants in a band that produced a sharp cutoff. Mello shows DOJ-originating funding increases discontinuously at the threshold while non-DOJ funding is smooth, satisfying the RD validity test. Cities just above the cutoff experience a ~3.2% police increase and a ~3.5% decline in cost-weighted crime. Two reasons it's the bar:

1. **Identification is RD, not DiD.** The cutoff rule provides quasi-random variation in treatment conditional on the running variable. This is the most credible identification design in the entire police-resources literature.
2. **The treatment is a discrete 2009 event, not staggered.** None of the Goodman-Bacon / CS / BJS critiques apply.

What Mello does *not* do: he doesn't test clearance, and he doesn't test detective staffing specifically. That is the open lane this project can credibly occupy.

---

## 3. Texas shock candidates, ranked by identification strength

### A — Clean and defensible

**A1. HB 1900 (87th Lege, 2021) and SB 23 (87th Lege, 2021): the "defunding penalty" laws.** This is the most under-exploited identification source in TX policing data. Both bills create a sharp 250,000-population threshold. HB 1900 imposes property-tax-rate caps, sales-tax revenue clawback, and 10-year annexation bans on any city >250K that the Governor's Public Safety Office determines has reduced its police-department appropriation. SB 23 (87R, 2021 — not to be confused with the 88R SB 23, which was a sentencing bill that died) requires voter approval before a >250K city can reduce police funding.

Texas has 11 cities >250K: Houston, San Antonio, Dallas, Austin, Fort Worth, El Paso, Arlington, Corpus Christi, Plano, Laredo, Lubbock. Roughly 30-50 cities sit in the 150K-249K band (Garland, Irving, Grand Prairie, McKinney, Frisco, Brownsville, Pasadena, Mesquite, Killeen, McAllen, etc.). That gives a workable bandwidth on either side of the cutoff.

*Threat-to-identification story:* (1) The cutoff is salient enough that cities just below it may pre-commit to police budgets to avoid future regulatory creep — meaning the comparison group is contaminated by behavioral anticipation. (2) Population is not a perfectly continuous variable; some cities sit on the cutoff for years. McCrary density tests will be needed. (3) The treatment is *budget-stickiness*, not detective staffing per se — the first-stage from HB 1900 → detective FTE must be established empirically, not assumed.

*Design feasibility:* Two complementary pieces.
- (i) **Pre/post 2021 difference-in-differences** comparing cities just above and below the 250K cutoff. The treatment date (Sept 1, 2021 effective date for HB 1900) is identical for all treated cities, so this is a **single-cohort DiD** and immune to the Goodman-Bacon problem. Use Roth-Sant'Anna honest pre-trends bounds for the parallel-trends assumption.
- (ii) **Regression-discontinuity on the 250K cutoff** using cross-sectional 2022-2025 data, with population as the running variable. This complements the DiD and exploits the same threshold but a different identifying assumption (smooth potential outcomes around the cutoff).

*Already published?* I find no peer-reviewed paper using HB 1900 as an identification source for any outcome. The bill is too new and its enforcement record is thin enough that academic attention hasn't gathered. This is the cleanest unclaimed identification opportunity in TX policing data.

**A2. Houston PD 2021-2022 homicide-division expansion (the SCM candidate).** Confirmed details: In March 2021, then-Chief Art Acevedo transferred ~20 property-crime detectives to investigate homicides. Mayor Sylvester Turner added six additional cadet classes in response to the 2020-21 homicide spike. Crime Scene Unit staff was scheduled to double under a five-year plan beginning in 2022. Houston PD's reported clearance jumped from 52% (2020) to 55% (2021) to 69% (2022).

*Threat-to-identification story:* The 2022 jump may partly reflect (a) reporting-convention changes during the SRS-to-NIBRS transition; (b) case-mix changes as the post-2020 homicide spike's outdoor / stranger / firearm-heavy cases worked through the system; (c) reverse causality (homicides falling makes per-detective workload drop, mechanically raising clearance). All three need to be controlled.

*Design feasibility:* Synthetic control on Houston using non-TX donor cities (Phoenix, San Diego, Philadelphia, Detroit, Memphis, Indianapolis, Charlotte). The treatment date is FY2021 (March 2021 detective transfer). Standard ADH (Abadie-Diamond-Hainmueller) or Ben-Michael augmented SCM. Placebo-test against the other large TX cities to verify Houston's gap is unique.

*Already published?* No academic paper has used the Houston 2021-22 reform as the treatment. The prior memo already flagged this and the conclusion holds.

### B — Workable with caveats

**B1. Dallas PD 2017-2018 detective contraction.** Detective count fell from ~28 (2017) to ~16 (2018) per CBS Texas reporting under Chief Reneé Hall, who was confirmed in office Sept 2017. Reporting from May 2019 confirms only 13 homicide detectives, with caseloads of 3-4 new cases per detective per month vs. the national average of 3-4 per detective *per year*. Hall resigned Sept 2020. Successor leadership (Chief García from 2021) rebuilt the unit; by 2024, Dallas reported 79% clearance.

*Threat-to-identification story:* (1) Hall's tenure was bundled with broader DPD instability — protest response, command staff shuffling, the Botham Jean case — so the detective contraction is not a clean staffing shock; it's a regime shock. (2) The 78% (2020) vs. 39% (FBI) clearance discrepancy makes the dependent variable unreliable. (3) Dallas has reported clearance figures (under Hall and under García) that the FBI doesn't appear to corroborate; the underlying measurement is suspect.

*Design feasibility:* Difference-in-differences with Houston, San Antonio, and Fort Worth as comparison cities, treatment date Sept 2017 (Hall's confirmation). Use case-level disposition data from PIA per the case-level-approach memo, not agency-reported clearance.

**B2. Austin PD 2020-2021 budget cut and 2021 reversal.** The Aug 2020 council vote cut $150M (one-third of APD's budget) and eliminated three cadet classes plus 150 vacant sworn positions. The August 2021 budget restored most of the cut after HB 1900 became binding. 210 APD officers retired/resigned in 2021 vs. 142 in 2020 vs. 68 in 2019. The 2020 cadet-class cancellation created a sworn-officer pipeline gap that persists through 2024-25. APD reported 100% homicide clearance in 2023 (the headline figure that turned out to coincide with low absolute homicide counts).

*Threat-to-identification story:* (1) Single-city, single-shock — only useful for SCM, not DiD. (2) APD stopped publishing yearly crime reports in 2021, so the dependent variable is unreliable without PIA. (3) Austin's reported 100% 2023 clearance contradicts the simple "fewer detectives → lower clearance" prediction, making this case a *Wellford-Cronin case-mix story* more than a staffing story.

*Design feasibility:* Synthetic control on Austin, treatment date Aug 2020, with non-TX donor cities. Useful as a robustness check on the Houston SCM (does the SCM machinery produce contradictory verdicts in two TX cities subject to opposite-signed shocks?).

**B3. COPS Hiring Program TX grants (staggered receipt).** The textbook staggered-DiD design — and exactly the case where the modern-DiD critique would bite if we used legacy TWFE. **As noted in your prompt**, the COPS program funds patrol, not detectives. The pass-through to detective bureau is theoretical and likely small. Police Funding Database shows recent TX COPS grants are sparse (the most visible recent award is a $250K FY25 grant to Dallas for accreditation planning, not patrol expansion). The 2009 ARRA-COPS wave that Mello exploited is the relevant treatment cohort, and that's now 17 years stale.

*Design feasibility:* If Brennan wants to do this, do it with Callaway-Sant'Anna explicitly. Pull the COPS grant database from USASpending.gov and code TX cities by year and dollar amount of COPS hiring grants. Treatment is positive grant receipt; outcomes are detective FTE and clearance. Multiple grant cohorts → staggered design → CS estimator. Expect a noisy null, because the patrol-to-detective pass-through is weak.

### C — Interesting but contaminated

**C1. Post-2020 retirement wave / Great Resignation.** Austin's 210 separations in 2021 are the most documented case in TX. Houston, Dallas, Fort Worth saw similar patterns but with less reporting. The contamination problem: the retirement wave occurred simultaneously with (a) the 2020 homicide spike, (b) the BLM protest aftermath, (c) HB 1900's enactment, (d) the NIBRS-transition reporting confusion. Disentangling the staffing-shock channel from those four other concurrent forces is essentially impossible.

**C2. 2023 DPS Austin patrol partnership.** From March to July 2023, DPS troopers deployed to Austin under an APD-DPS partnership; the deal ended after a trooper shot a fleeing suspect on July 10, 2023. The partnership was patrol-focused, not investigative, and there's no documented diversion of APD detectives. It's interesting as a measurement issue (DPS-conducted arrests showed up in APD jurisdiction data) but not as a detective-staffing shock.

**C3. Austin disannexations 2024 (HB 3053 elections).** Six neighborhoods, ~2 square miles total, voted on disannexation in August-November 2024. The largest was Lost Creek. Population and homicide impact are trivial (Austin's homicide caseload is overwhelmingly in the central and eastern crescents, not Lost Creek). Not a workable identification shock.

**C4. Hurricane Harvey 2017 Houston displacement.** Harvey displaced ~30,000 people and damaged the criminal-justice infrastructure (courts displaced; cases dismissed). It's plausibly a caseload-denominator shock for HPD homicide, but the population was largely re-housed within Houston, and the displacement signal is dominated by the simultaneous court-system disruption. Useful as a robustness placebo (Harvey should not produce a clearance jump similar to the 2021-22 expansion); not workable as a primary treatment.

**C5. State takeovers / DOJ pattern-and-practice.** None of the major TX agencies are currently under a DOJ pattern-or-practice consent decree. No federal monitor on Houston PD, Dallas PD, Austin APD, or SAPD. This is a non-shock in TX during the relevant period.

**C6. SAPD, Camp Bullis-area annexation.** San Antonio's Camp Bullis annexations are small in jurisdictional terms relative to SAPD's total caseload. Same logic as Austin disannexations — not a workable shock.

**C7. Project Safe Neighborhoods / Strategies for Policing Innovation TX waves.** Both programs operate in TX (PSN runs through multiple federal judicial districts; SPI has had TX awardees historically), but neither maintains a publicly enumerated TX-city-by-year award list that's easy to merge with detective-staffing data. The TX governor's eGrants portal is the place to start. Worth a focused pull, but the within-program variation in treatment intensity is large enough that even a clean DiD will struggle to attribute clearance changes to PSN or SPI rather than the broader policing context.

---

## 4. Recommended primary identification strategy + robustness design

**Primary: HB 1900/SB 23 250K-population RD-DiD.**

The combined HB 1900 + SB 23 framework gives a sharp legal cutoff (effective Sept 1, 2021) that applies to 11 TX cities and not to ~30-50 cities just below. The cleanest specification is a **stacked / single-cohort difference-in-differences with population-eligibility-as-treatment**, with case-level homicide clearance as the dependent variable (per `docs/case-level-approach.md`), and a parallel **regression discontinuity at the 250K cutoff** as the cross-sectional corroboration.

Concrete specification sketch:
- **Treatment:** Indicator for city population >250,000 as of 2020 Census × post-Sept-2021 dummy.
- **Outcome:** Case-level homicide clearance, coded from PIA pulls (per case-level memo). Both total clearance and clearance-by-arrest separately, to falsify against reporting effects.
- **First stage:** Detective bureau FTE per homicide, from PIA pulls. Establish that HB 1900 *did* change detective staffing in treated cities, not just aggregate budget. If the first stage is weak, fall back to a reduced-form interpretation: "we estimate the effect of a credible threat of state intervention on clearance."
- **Estimator:** Single-cohort DiD (Sept 2021 effective date for all treated cities) → standard 2x2 DiD with year/city FE is fine. *No staggered-DiD critique applies.* Robustness with CS estimator anyway (it should reproduce the 2x2 DiD result exactly when there's one cohort).
- **Pre-trends:** Roth-Sant'Anna honest sensitivity analysis, not just an event-study plot. Pre-register the bound (e.g., maximum slope deviation we're willing to tolerate in the pre-period before declaring parallel trends violated).
- **Bandwidth:** RD bandwidth specifications at ±10%, ±25%, ±50% of the 250K cutoff (so populations 225K-275K, 187K-312K, 125K-375K). Pre-commit to the ±25% bandwidth as the primary.
- **Falsification tests:** (a) McCrary density test on city population around 250K. (b) Treatment-effect heterogeneity by victim race — Bjerk's null is across all race groups; if our effect is conditional on demographics, that's a story. (c) Placebo treatment date (Sept 2019) — should produce a null.

**Robustness design: Houston PD 2021-2022 synthetic control.**

Use Houston as a within-state corroboration of the RD-DiD result. If HB 1900 truly bound TX cities into police-budget stickiness post-2021, the Houston SCM should *not* show a Houston-specific 2021-22 effect that exceeds the cross-TX response; if Houston's homicide-division reform produced clearance gains over and above what HB 1900 produced statewide, the SCM will isolate that. Donor pool: non-TX cities of >500K population not subject to similar reforms (Phoenix, Indianapolis, Charlotte, Memphis, Detroit, San Diego, Philadelphia, Columbus, Jacksonville). Treatment date: March 2021 (Acevedo's detective transfer). Use Ben-Michael's augmented SCM with covariate adjustment for case-mix.

If both designs return the same sign and similar magnitudes, the joint inference is much stronger than either alone. If they disagree, the disagreement is itself the contribution (e.g., "Houston's reform mattered above and beyond the statewide budget-stickiness imposed by HB 1900").

---

## 5. What the pre-analysis plan must commit to before any data pull

Following the recommended pre-registration approach in `docs/literature-review.md` §6 and `docs/case-level-approach.md` §recommended-next-steps:

1. **Outcome definition.** Pre-specify clearance as "case cleared by arrest, coded from PIA-pulled case-level data, where the disposition is unambiguously an arrest leading to charges filed." Code clearance-by-exception as a *separate* outcome. Pre-commit to running the model on both, with the arrest-only outcome as primary and the total-clearance outcome as a falsification test for reporting effects.
2. **First-stage commitment.** Define the detective-FTE measure explicitly: PIA-pulled headcount of sworn officers assigned to the homicide unit on Dec 31 of each year, by city. Pre-commit to reporting the first-stage F-statistic and to a reduced-form interpretation if the first stage is weaker than F=10.
3. **RD bandwidth.** Primary specification at ±25% of the 250K cutoff (population 187K-312K). Secondary at ±10% and ±50% as robustness. No data-driven optimal bandwidth selection (Imbens-Kalyanaraman) without pre-commitment — pre-specify that we're reporting one optimal-bandwidth specification as a single robustness column, not as the primary.
4. **Pre-trends.** Pre-commit to Roth-Sant'Anna honest pre-trends sensitivity bounds. Pre-specify M-bar (the maximum-slope-deviation parameter). If the post-period effect is robust to M-bar = the 75th percentile of pre-period slope changes, declare honest parallel trends satisfied.
5. **Stopping rules.** Pre-specify the threshold at which we declare the thesis "supported," "ambiguous," or "rejected." Suggested: a 95%-CI on the DiD coefficient that excludes zero in the *correct* direction = supported; a 95%-CI that includes zero but excludes the bottom 25% of plausible effect sizes from the literature = ambiguous; a 95%-CI that includes both zero and large negative values = rejected.
6. **Comparison-city pre-commitment for the SCM.** Pre-specify the donor pool (the 9 cities listed above) and the pre-period match window (e.g., 2015-2020 monthly clearance trajectory). Do not iterate on the donor pool after seeing the post-2021 trajectory.
7. **Multiple-hypothesis correction.** Pre-specify the family of hypotheses (HB 1900 main effect, Houston SCM, racial-disparity heterogeneity, exceptional-clearance falsification). Apply Bonferroni or Romano-Wolf correction depending on the number of tests. Pre-register the correction.
8. **Conflict-of-interest and political-pressure disclosure.** Texas Appleseed's involvement in advocacy on policing creates an editorial perception risk. The pre-analysis plan should be hosted publicly on OSF before data arrive, and the plan should commit to publishing the null result if that's what the data show.

---

## Bibliography (new in this memo)

Borusyak, K., Jaravel, X., & Spiess, J. (2024). "Revisiting Event-Study Designs: Robust and Efficient Estimation." *Review of Economic Studies* 91(6): 3253-3285. https://academic.oup.com/restud/article/91/6/3253/7601390

Callaway, B., & Sant'Anna, P. H. C. (2021). "Difference-in-Differences with multiple time periods." *Journal of Econometrics* 225(2): 200-230. https://www.sciencedirect.com/science/article/pii/S0304407620303948

Chalfin, A., Hansen, B., Weisburst, E. K., & Williams, M. C., Jr. (2022). "Police Force Size and Civilian Race." *American Economic Review: Insights* 4(2): 139-158. https://www.aeaweb.org/articles?id=10.1257/aeri.20200792

de Chaisemartin, C., & D'Haultfœuille, X. (2020). "Two-Way Fixed Effects Estimators with Heterogeneous Treatment Effects." *American Economic Review* 110(9): 2964-2996. https://www.aeaweb.org/articles?id=10.1257/aer.20181169

Evans, W. N., & Owens, E. G. (2007). "COPS and crime." *Journal of Public Economics* 91(1-2): 181-201.

Goodman-Bacon, A. (2021). "Difference-in-differences with variation in treatment timing." *Journal of Econometrics* 225(2): 254-277. https://www.sciencedirect.com/science/article/abs/pii/S0304407621001445

Roth, J., Sant'Anna, P. H. C., Bilinski, A., & Poe, J. (2023). "What's trending in difference-in-differences? A synthesis of the recent econometrics literature." *Journal of Econometrics* 235(2): 2218-2244. https://www.jonathandroth.com/assets/files/DiD_Review_Paper.pdf

Rambachan, A., & Roth, J. (2023). "A More Credible Approach to Parallel Trends." *Review of Economic Studies* 90(5): 2555-2591. https://www.jonathandroth.com/assets/files/HonestParallelTrends_Main.pdf

Sun, L., & Abraham, S. (2021). "Estimating dynamic treatment effects in event studies with heterogeneous treatment effects." *Journal of Econometrics* 225(2): 175-199.

Weisburst, E. K. (2019). "Patrolling Public Schools: The Impact of Funding for School Police on Student Discipline and Long-term Education Outcomes." *Journal of Policy Analysis and Management* 38(2): 338-365. https://onlinelibrary.wiley.com/doi/abs/10.1002/pam.22116

Weisburst, E. K. (2024). "Whose Help Is on the Way? The Importance of Individual Police Officers in Law Enforcement Outcomes." *Journal of Human Resources* 59(4): 1122-1149. https://jhr.uwpress.org/content/early/2022/03/01/jhr.0720-11019R2

Wooldridge, J. M. (2021). "Two-Way Fixed Effects, the Two-Way Mundlak Regression, and Difference-in-Differences Estimators." Working paper / forthcoming. https://www.researchgate.net/publication/354015780

**Texas laws and primary sources:**

Texas Local Government Code Chapter 109, "Determination of Defunding Municipalities." https://statutes.capitol.texas.gov/Docs/LG/htm/LG.109.htm

Texas HB 1900, 87th Legislature, Regular Session (2021), enrolled text. https://www.legis.state.tx.us/tlodocs/87R/billtext/html/HB01900F.HTM and bill analysis https://capitol.texas.gov/tlodocs/87R/analysis/html/HB01900H.htm

Texas SB 23, 87th Legislature, Regular Session (2021). https://legiscan.com/TX/supplement/SB23/id/165582

Office of the Texas Governor, Public Safety Office, "Application for Exception for Certain Reductions to Municipal Police Department Budget." https://gov.texas.gov/organization/cjd/police-department-budget-exception-application

Police Funding Database (LDF/TMI), Texas page. https://policefundingdatabase.org/explore-the-database/locations/texas/grant-funding

GAO-13-521, Community Policing Hiring Grants. https://www.gao.gov/products/gao-13-521

**Texas reporting on shocks:**

Texas Tribune (2021), "Texas' larger cities would face financial penalties for cutting police budgets." https://www.texastribune.org/2021/05/06/texas-police-budget-cuts-legislature/

KUT Radio (2021), "Last Year Austin Cut Its Police Budget By Millions. A New State Law Means It'll Likely Reverse That Move This Week." https://www.kut.org/austin/2021-08-11/last-year-austin-cut-its-police-budget-by-millions-a-new-state-law-means-itll-likely-reverse-that-move-this-week

ABC13 Houston (2021), "Houston PD officers being moved to homicide division to deal with crime influx." https://abc13.com/houston-crime-homicide-rate-police-department-understaffed/10422191/

Click2Houston (2022), "Houston police solving more homicide cases compared to last year." https://www.click2houston.com/news/local/2022/05/10/houston-police-solving-more-homicide-cases-compared-to-last-year-department-says/

The Austin Chronicle (2023), "State Trooper Deployment Targeted Black and Brown Neighborhoods with Unclear Effect on Crime." https://www.austinchronicle.com/news/2023-12-15/state-trooper-deployment-targeted-black-and-brown-neighborhoods-with-unclear-effect-on-crime/

KUT Radio (2023), "Austin again suspends its patrol partnership with DPS." https://www.kut.org/crime-justice/2023-07-12/austin-again-suspends-its-patrol-partnership-with-dps

Fox 4 Dallas (2024), "Dallas police solved nearly 80% of its homicide cases last year." https://www.fox4news.com/news/dallas-police-2024-homicide-cases

KERA News (2025), "Dallas police officials want 300 more officers — but warn any more could be too costly." https://www.keranews.org/news/2025-02-19/dallas-police-officials-want-300-more-officers-but-warn-any-more-could-be-too-costly

---

## Items flagged as uncertain and worth verification

- **Specific text of Bjerk's IV first-stage specification.** I confirmed via multiple secondary sources that Bjerk uses lagged-budget and state-revenue-shock IVs and reports OLS plus probit estimates with city and year fixed effects. The full structural form of the IV was not retrievable without paywalled JELS access. Verify against the published PDF (Bjerk's posted version is at https://static1.squarespace.com/static/5b7ea2794cde7a79e7c00582/t/64740df855cded580bccb3c4/1685327353164/does+greater.pdf) before any methodological claim is published.
- **Exact COPS Hiring Program TX-by-city-by-year table.** The Police Funding Database's TX page enumerates only 23 grants total for FY16-FY26, of which most are state-level rather than COPS Hiring grants to municipal departments. The fuller table is on USASpending.gov but requires API-style queries. Pull this directly before relying on COPS-grant variation as a robustness identification.
- **Confirmation that the Governor's PSO has issued *any* HB 1900 defunding determination.** I located the legal framework and the public-facing exception-application portal, but no published list of cities formally determined to be "defunding municipalities" under the act. As of mid-2026, the enforcement record may be thin (most >250K cities scrambled to comply pre-emptively after HB 1900's enactment, which is actually consistent with the strong-first-stage story for our RD-DiD design). Confirm with a PIA to the PSO and/or a Texas Public Information Act request to the Comptroller's Office regarding any sales-tax-withholding actions taken under HB 1900.
- **Houston PD detective-bureau FTE year-over-year.** Public reporting confirms the March 2021 transfer of ~20 property-crime detectives and the addition of six cadet classes, but the annual homicide-unit headcount is not in published budget documents at the level of detail we need. Will require PIA to HPD records.
- **Dallas detective-bureau FTE year-over-year under Hall (2017-2020).** CBS Texas reports 28→16 in 2017-18; the May 2019 figure of 13 detectives appears in NBC DFW reporting on the Bryan Riser case. The original primary-source documentation for the 28-figure is harder to locate. Verify before relying on the magnitude.

---

## Appendix: No modern-DiD replication of Evans & Owens (2007) exists

A focused literature search (May 2026) confirms that **no published replication of Evans & Owens (2007, *Journal of Public Economics*) using modern staggered-DiD estimators (CS, SA, BJS, dCDH, Wooldridge ETWFE) appears to exist.** The search covered *Journal of Public Economics*, *AEJ: Applied*, NBER, SSRN, IZA, ProQuest dissertations, and the Evans-Owens Google Scholar cited-by list filtered for 2021+ methodological terms (zero post-2021 cited-by hits on those filters, which is itself diagnostic).

The methods papers themselves do not use Evans-Owens as an application. Roth, Sant'Anna, Bilinski & Poe (2023)'s policing example is a *training* program, not COPS hiring. Goodman-Bacon (2021), Callaway-Sant'Anna (2021), Sun-Abraham (2021), Borusyak-Jaravel-Spiess (2024), and de Chaisemartin-D'Haultfœuille (2020) skip it.

**Closest existing fragility evidence:**

- **Worrall & Kovandzic (2007), *Criminology* 45(1): 159-190** — found no discernible effect on serious crime using a different panel structure. Pre-modern DiD, but a direct contradiction of Evans-Owens's central elasticities.
- **Mello (2019)** is *not* a methodological replication. Different shock (2009 ARRA), different design (application-score RD/DiD). Broadly consistent effect sizes are reassuring on direction, not on the original weighting.
- **Gunderson, Cohen, Schiff, Clark, Glynn & Owens (2021), *Nature Human Behaviour* 5: 194-204** — knocked down Bove & Gavrilova (2017) on the 1033 militarization program. Data rather than weighting grounds, but the closest published analogy of a canonical policing-grant causal estimate failing on re-examination.
- **Chalfin & McCrary (2018)** has a narrow computational replication by Cunningham et al. (2024, *Journal of Applied Econometrics* 39(1): 217-224), but that confirms results; it is not a staggered-DiD reweighting.

**Caveat on what is actually vulnerable in Evans-Owens.** Their preferred specification is **2SLS using grant dollars as an instrument for sworn officers**, not pure TWFE event study. The Goodman-Bacon critique hits their reduced-form DiD specs hardest; the IV is somewhat insulated. A modern-methods re-estimation would more likely shrink magnitudes than flip signs.

**Implications.**

1. **Citation strategy.** When this project needs to lean on a police-staffing-→-crime causal benchmark, lead with **Mello (2019)** or **Chalfin & McCrary (2018, *REStat*)** rather than Evans-Owens. Their identification doesn't carry unresolved staggered-TWFE baggage.
2. **Standing of the broader COPS-grant literature.** This confirms the §1 audit's headline: there is an unclaimed methodological gap in the entire COPS-grant causal literature. A CS or BJS re-estimation of the 1990-2001 Evans-Owens panel would be a legitimate short methods paper on its own.
3. **Project-scope note.** That gap is a distinct side-quest from the TX homicide-clearance work. Flagged for awareness; not in scope unless deliberately added later.
