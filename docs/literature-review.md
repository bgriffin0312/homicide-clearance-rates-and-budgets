# Homicide Clearance, Detective Staffing, and Causal Identification: A Literature Review for the Texas Project

Prepared for Brennan Griffin, May 2026.
Scope: synthesizing the empirical work on whether detective staffing and resources move homicide clearance rates, what swamps that effect, what natural experiments have been used, and what Texas-specific evidence exists.

---

## TL;DR

- The literature is unambiguous on one thing: case characteristics (witness availability, victim-offender relationship, weapon, neighborhood disadvantage, time-to-discovery) explain far more variation in clearance than anything police departments can control. Detective staffing matters, but the case-mix variables dwarf it.
- Two large multisite studies (Wellford & Cronin 1999/2000; Wellford, Lum, Scott, Vovak & Scherer 2019) and one well-identified within-city evaluation (Braga & Dusseault 2018 on Boston) find that *organizational* features — squad size, supervision quality, peer review, first-responder protocols, time-to-detective-assignment — produce real but modest clearance gains, on the order of 10-20 percentage points when implemented as a bundle.
- The cleanest *causal* econometric paper in the space, Bjerk (2022, JELS), finds *no* effect of police-budget changes on homicide clearance using OLS or IV across 50 large cities, 2007-2017. This is the single most important paper for Brennan to internalize, because it argues against his thesis at exactly the unit of analysis he's contemplating.
- The "great decline" debate (Cook & Mancik 2024 Annual Review; Cook & Lopez 2024) argues most of the 60-year drop in clearance reflects a *rising evidentiary standard for arrest*, not falling police effort. If that's right, clearance is a degraded performance metric.
- Texas-specific clearance numbers are unreliable in their raw form: Dallas reported 78% for 2020 while FBI records showed 39%; Houston jumped from 52% (2020) to 69% (2022); Austin reported 100% for 2023 but stopped publishing yearly reports altogether in 2021. Brennan needs to pin down each agency's clearance-by-exception practices before any cross-city comparison is meaningful.

---

## What the literature establishes (with magnitudes where available)

### 1. The foundational studies

**Greenwood, Chaiken & Petersilia, RAND (1975-1977).** The original critical reappraisal of detective work. Surveyed 153 large police departments and ran detailed case-flow analyses in 25. Headline findings: investigators spent only about 7% of their time on activities that directly led to clearances; most cleared cases were solved by initial patrol-officer information collection or by tips from the public, not by post-assignment detective work. The implication for Brennan: marginal detective staffing may matter much less than the quality of the *first responding officer's* report and witness canvass. RAND argued for reallocating detectives to fewer, more solvable cases — the intellectual root of "case screening" and "solvability factors."

**Eck, Solving Crimes (PERF, 1983).** Used investigative data on ~320 robberies and ~3,360 burglaries in DeKalb County, GA; St. Petersburg, FL; and Wichita, KS. Eck refined Greenwood's conclusion: detectives matter, but their marginal product is decreasing — the most productive detective hour is the first one spent on a "highly solvable" case (one with a named suspect, identifiable witness, traceable property). Solvability factors became standard case-screening practice. Eck's later "new detective" essay (2019, *Criminology & Public Policy* 18) is a companion piece to the Wellford et al. 2019 study and is worth a read for the framing alone.

**Wellford & Cronin (1999), *An Analysis of Variables Affecting the Clearance of Homicides: A Multisite Study* (NIJ).** The most influential homicide-specific study of the pre-2000 era. Analyzed 798 homicides from 1994-95 in four large unnamed cities (selected from the 20 largest based on stable clearance patterns), plus FBI panel data on 170 cities, 1980-1994. Key findings on staffing: agencies that assigned **three or four detectives to the initial scene** had higher clearance odds than those assigning one or two. Note this is *initial assignment* — not a per-case ratio over the life of the investigation. Beyond staffing, the strongest predictors of clearance were patrol-officer first-response actions (securing scene, identifying witnesses, initiating neighborhood canvass) and rapid notification of detectives, evidence technicians, and the medical examiner. Cases harder to clear: Black or Hispanic victims, outdoor location, no eyewitness, drug or gang motive, firearm, weapon found at scene. 50% of closed cases solved within a week; 93% within a year.

**Wellford, Lum, Scott, Vovak & Scherer (2019), "Clearing Homicides," *Criminology & Public Policy* 18(3): 553-600.** The 20-year follow-up. Examined 30 large U.S. cities and case-level data from 50 agencies; overall clearance across the sample was 63%. High-clearance agencies were distinguished by community-relations strength, in-house crime/intelligence analysis, organizational ethos of collaboration with patrol, and adequate staffing/training. Critically, the authors emphasize that no single factor dominates — clearance is multiply determined and the gains from any one reform are bounded. The companion piece, Scott, Wellford, Lum & Vovak (2019), *Police Quarterly* 22(1): 82-111, documents that clearance-rate variability across U.S. agencies is enormous and only partially explained by case mix.

**Carter & Carter (in the cold-case domain).** I could not confirm a specific Carter & Carter 2016 publication on the staffing of cold-case units from open sources — flagging this for verification. The general consensus from the broader cold-case literature (e.g., PERF, IACP cold-case toolkit; Davis, Jensen, Burgette and colleagues) is that dedicated cold-case units staffed with even 2-3 full-time investigators clear materially more old cases than ad-hoc reassignment to active detectives — but cold-case clearance is a different production function (new information from witnesses, DNA, genealogy) than fresh-case clearance.

### 2. Recent within-city evaluations

**Braga & Dusseault (2018), "Can Homicide Detectives Improve Homicide Clearance Rates?" *Crime & Delinquency* 64(3): 283-315.** The Boston PD reform of January 2012 added detectives to the homicide unit, standardized investigative protocols, instituted monthly peer review of open cases, added forensic-tech presence at scenes, and improved victim-witness services. Clearance rose from 47% (5-year pre-reform average) to 57% (3-year post) in the headline analysis. A later evaluation cited in Braga's *Manhattan Institute* review (2021) reports clearance hitting 66% in 2012-14, with the effect concentrated in the hard-to-clear cases (young Black male victims, outdoor, gang-involved), where clearance roughly doubled from 27% to 43%. This is the strongest within-city "package" evaluation in the literature, but it is a bundled reform — you cannot cleanly separate the additional detectives from the protocol changes.

**Braga, Turchan & Barao (2019), "The Influence of Investigative Resources on Homicide Clearances," *Journal of Quantitative Criminology* 35(2): 285-318.** Analyzed 465 Boston homicides, 2007-2014. Found a strong association between specific investigative actions (forensic testing, witness re-interviews, search warrants) and clearance probability, controlling for case characteristics. Investigative effort post-48 hours is where homicide vs. nonfatal-shooting clearance diverges.

**Cook, Braga, Turchan & Barao (2019), "Why do gun murders have a higher clearance rate than gunshot assaults?" *Criminology & Public Policy* 18(3): 525-551.** Same Boston data. Within the first 48 hours, gun homicides and nonfatal gun assaults cleared at identical rates (11%). After 48 hours, an additional 32% of homicides cleared vs. only 8% of nonfatal shootings — entirely attributable to *sustained investigative effort* on homicides. This is the cleanest empirical argument that effort produces clearance at the margin, holding case type roughly constant.

**Hsu, Emerick & Sytsma (2024), "Police personnel allocation and homicide clearance," *Policing: An International Journal* 47(5): 786-803.** Panel of 100 largest U.S. cities, 2000-2013, with random-effects regression and an operations-management "optimum analysis." Find both patrol and investigative personnel levels significantly associated with homicide clearance, and that reallocating marginal officers from patrol to investigations would raise clearance. The identification is observational and worth scrutiny — they're not exploiting an exogenous shock — but it points the same direction as Braga's Boston evidence.

### 3. What kills clearance: the case-mix story

Roberts (2007, *Homicide Studies*) and Roberts (2015, *Homicide Studies* 19(3): 273-300, "Adjusting Rates of Homicide Clearance by Arrest for Investigation Difficulty") quantified how much agency-level clearance rates change when you control for case mix. Of 85 agencies in his 2015 paper, **16% would be miscategorized as above- or below-average performers** if you used raw clearance rates instead of difficulty-adjusted ones. The case-mix variables (victim demographics, location, weapon, relationship, neighborhood) absorb the bulk of explained variance.

Mancik, Parker & Williams (2018, *Homicide Studies* 22(2): 188-213) added the most rigorous neighborhood-level evidence: in Chicago, **collective efficacy** (a measure of informal social cohesion and willingness to intervene, from the PHDCN survey) was a statistically significant positive predictor of clearance, while economic disadvantage and residential instability significantly depressed it.

Campedelli (2024, *Criminology* 62(3): 587-619) extended the racial-disparity finding to a national sample: clearance is **3.4 to 4.8 percentage points lower for homicides involving Black victims**, even after extensive case-level controls. The neighborhood analysis paper in *J. Criminal Justice* 98 (2025) using 50 cities and 15,557 census tracts confirms that economic disadvantage and Black population share are associated with lower clearance across neighborhood types.

Brookman, Maguire & Maguire (2019, *Homicide Studies* 23(2): 145-174) is the qualitative counterpart — interviews with U.S. and British homicide detectives — and reinforces that witness cooperation is the binding constraint detectives perceive most often. U.K. clearance never fell below ~90% even as U.S. rates collapsed, which the authors attribute partly to organizational structure (career detective specialization, slower case assignment, more dedicated forensic capacity) and partly to weaker U.S. witness-protection infrastructure.

**Brennan, take this seriously:** If you build a multivariate model with even a modest set of case-mix controls — victim race/sex/age, weapon type, location (indoor/outdoor), known relationship, drug/gang flag, neighborhood disadvantage index — you will likely soak up 60-70% of the variance before your detective-FTE variable enters. The detective-staffing coefficient that survives that gauntlet, *if any*, is what you'll be reporting. Be ready for the estimate to be statistically insignificant or imprecisely estimated, particularly with the modest sample of Texas cities.

### 4. The cleanest econometric paper goes the other way

**Bjerk (2022), "Does greater police funding help catch more murderers?" *Journal of Empirical Legal Studies* 19(3): 528-559.** This is the paper that should give Brennan the most pause. Panel data on homicides in roughly 50 of the largest U.S. cities, 2007-2017. OLS and IV specifications (using lagged budget variation and state-level revenue shocks). Headline: **no detectable effect of police funding on homicide clearance.** Robust to alternative budget measures (total police budget, sworn officers per capita) and across victim race and neighborhood type. Bjerk explicitly engages the reverse-causality concern Brennan raised. The paper does not separate detective from patrol allocation, so there is a back door for Brennan's thesis — but he must address Bjerk head-on, ideally by showing that *detective* allocation behaves differently than aggregate budget.

### 5. The "rising arrest standard" interpretation

**Cook & Mancik (2024), "The Sixty-Year Trajectory of Homicide Clearance Rates: Toward a Better Understanding of the Great Decline," *Annual Review of Criminology* 7: 59-83**, plus **Cook & Lopez (2024), "Explaining the Extraordinary Decline in Chicago's Homicide Arrest Rates, 1965 to 1994 and Beyond," *Journal of Contemporary Criminal Justice* 40(2).** Together they argue the long-run clearance decline is largely benign: case-mix change (more strangers, more guns outdoors, fewer domestic murders) explains part of it, but the bigger driver is that **prosecutors and police raised the operational standard for an arrest.** In Chicago, the prison-to-arrest ratio rose sharply over the same period clearance fell, meaning each arrest now produces a conviction more reliably than it did. If they're right, clearance is a noisy proxy for police productivity, and Brennan's regressor (staffing) and dependent variable (clearance) may be partially decoupled by changes in prosecutorial behavior. This is a problem worth a paragraph in any pre-analysis plan.

### 6. The police-staffing-and-crime literature is adjacent, not on-point

The Chalfin & McCrary (2018, *Review of Economics and Statistics*) and Mello (2019, *J. Public Economics*) papers find robust *negative* effects of police staffing on crime (Chalfin-McCrary elasticity of about -0.34 for violent crime; Mello -1.3) using IV / RD identification off the COPS Hiring Program. **Neither tests clearance.** Brennan should cite them for the proposition that "police staffing matters causally for something," then acknowledge that the specific clearance link is much weaker in the existing literature.

---

## Where the literature is thin or contested

1. **Detective-specific staffing.** Almost no published paper isolates *homicide detective FTEs* from aggregate sworn officers or aggregate budget. Wellford et al. (2019) and Hsu et al. (2024) are the closest, but neither has clean causal identification. There is a genuine gap in the literature that a Texas-cities PIA project could fill, *if* the data come back clean.

2. **Workload (cases per detective per year).** Eck pushed this in 1983; Wellford et al. nodded to it; no one has produced a defensible estimate of the marginal effect of an extra case per detective per year on solve probability. Brennan could be the person who does, if he can get accurate caseload data.

3. **Time-to-detective-assignment.** Wellford & Cronin (1999) and Wellford et al. (2019) both identify this as a strong correlate, but no one has exploited a within-city policy change in assignment protocol as a natural experiment.

4. **Civilian-staff multiplier.** Both Boston (crime analysts added) and the PERF best-practices literature suggest civilian crime analysts may have higher marginal product than additional sworn detectives. This is essentially untested in the causal literature.

5. **The dose-response curve.** We do not know whether the staffing effect is linear, concave, or has a threshold (e.g., does adding a 4th detective per scene matter as much as the 3rd? Wellford & Cronin implied a threshold; no one has tested it rigorously).

---

## Natural experiments already used in this space

| Shock / design | Citation | What it estimated | Result |
|---|---|---|---|
| COPS Hiring Program 2009 RD (funding score cutoffs) | Mello (2019), *JPubE* | Police staffing → crime | -1.3 elasticity violent crime; not on clearance |
| COPS hiring panel IV | Chalfin & McCrary (2018), *REStat* | Police staffing → crime | -0.34 elasticity violent crime; not on clearance |
| Boston PD homicide reform (Jan 2012) | Braga & Dusseault (2018); Braga, Turchan & Barao (2019) | Bundled reform → clearance | +10 to +19 pp clearance, concentrated in hard cases |
| Project Safe Neighborhoods funding (post-2001) | Multiple, e.g., McGarrell et al.; RTI national eval | PSN funding → violent crime | Significant violence reduction in treated cities; clearance not the primary outcome |
| Police de-prosecution policy (Philadelphia, 2015 onward) | Hogan (2022), *Criminology & Public Policy* | Prosecutor policy → homicide rate | Synthetic-control; large homicide increase. Adjacent, but illustrates the SCM template Brennan could use. |
| Bjerk panel & IV, 2007-2017 | Bjerk (2022), *JELS* | Police budget → clearance | Null |
| Hsu, Emerick & Sytsma panel, 2000-2013 | *PIJPSM* (2024) | Personnel allocation → clearance | Positive correlation, observational only |

**For Brennan specifically:** The cleanest Texas natural-experiment candidates I see are (a) the post-Floyd 2020-21 budget shifts in Austin (the council's $150M reallocation, then partial restoration), which produced a sharper detective-pipeline disruption than peer cities; (b) Houston PD's 2021-22 homicide-unit expansion ("expanded homicide department" was credited for the 52% → 69% clearance jump — this is the most promising synthetic-control candidate in the state); and (c) Dallas's 2017-2018 detective collapse (28 → 16 homicide detectives in one year under Chief Hall). All three are *bundled* shocks, but the Dallas case in particular has the right structure for a difference-in-differences or synthetic control comparison against San Antonio and Fort Worth, which did not experience an analogous detective-bureau contraction.

---

## The endogeneity problem (and the cleanest published treatments)

The fundamental problem: cities with more homicides either (a) hire more detectives in response, biasing OLS toward a positive coefficient on staffing, or (b) face fiscal distress that simultaneously depresses both staffing and clearance, biasing OLS toward a *negative* coefficient. Both directions of bias are alive.

The cleanest published responses are:

- **Bjerk (2022)** — uses lagged budget variation and state revenue shocks as instruments. Finds null. Whatever Brennan does, he needs to either replicate Bjerk's IV at the Texas city-year level or argue why he can't.
- **Mello (2019)** — RD on COPS funding scores. The cleanest identification in the broader police-effects literature, but for crime, not clearance.
- **Braga & Dusseault (2018)** — within-city pre-post with comparison series. The structural assumption is that whatever was changing in Boston was not also changing in the comparison cities. Plausible for Boston in 2012; less plausible in Texas in 2020-21 when every city was simultaneously shocked.

Brennan's best identification strategies, in order of credibility:
1. **Synthetic control on Houston (2021-22 homicide unit expansion).** Build a donor pool from peer non-Texas large cities not undergoing similar reform. Test clearance trajectory.
2. **Difference-in-differences on Dallas (2017-18 detective collapse).** Houston, San Antonio, Fort Worth as comparison.
3. **Bartik-style shift-share** using lagged state revenue interacted with city dependence on state aid, as an IV for police budget. Bjerk-style.
4. **Within-city detective-rotation experiment.** If any TX department has rotated detectives in/out of the homicide unit on identifiable dates, that's a natural staffing shock at the squad level. This requires PIA data that may or may not exist.

---

## Measurement landmines

1. **Clearance by exception** — Under UCR rules, a case is cleared when (a) an arrest is made *or* (b) the offender is identified but cannot be prosecuted (dead, jurisdictional barrier, victim refusal, etc.). Departments vary enormously in how aggressively they invoke exceptional clearance. ProPublica's 2018 rape-clearance investigation found agencies clearing 40%+ of rape cases by exception with no charges filed; the practice is at least as widespread in homicide. **For any Texas city, Brennan should ask in his PIA: "For each year, the number of homicides cleared by arrest and the number cleared by exceptional means, separately."**

2. **The Dallas-FBI discrepancy.** CBS Texas (2023) documented that Dallas PD self-reported 78% homicide clearance in 2020 while FBI records showed 39%. This is a 39-point gap. Some of it is reporting lag (a case cleared in 2022 still counts toward 2020 in DPD's books but appears in 2022 FBI data). Some of it may be coding differences. Either way, **never trust a single-year cross-sectional clearance number without understanding the agency's reporting convention.**

3. **NIBRS transition (2021).** The FBI switched from SRS to NIBRS reporting on Jan 1, 2021. Only 66% of agencies reported in NIBRS format that year; ~40% of large-city data is missing or incomplete in the 2021 federal data. Texas's TXUCR system continued reporting throughout but cannot be cleanly merged with national panels for 2020-2022 without manual reconciliation.

4. **Multi-year accounting.** Most departments report a year's clearance rate as (homicides occurring in year Y that are now cleared) / (homicides occurring in year Y). Cases solved years later get credited backward. This biases recent-year clearance rates *downward* artificially. For trend analysis, Brennan needs to know whether each city reports on an occurrence-year or report-year basis, and whether they update past years' figures.

5. **The Murder Accountability Project critique.** Tom Hargrove's MAP, using FBI SHR data, argues clearance rates are systematically overstated in many agencies because of exceptional-clearance abuse and underreporting of homicides to the SHR. MAP also flags ~5,000 missing-from-SHR homicides per year. Worth citing as a measurement caveat and worth pulling MAP's Texas-city-level data as a sanity check.

6. **Adamson & Rentschler (2025), "How policing incentives affect crime, measurement, and justice," *Economic Inquiry* 63(2): 545-567.** A formal-theoretic / experimental piece showing that clearance rate as a performance measure can *invert* — under certain incentive regimes, police "perform better" on clearance precisely when they are doing worse on the underlying justice outcome (false arrests, unsolved real cases). This is the most sophisticated theoretical critique of clearance as a metric. Cite it.

7. **The Cook arrest-standard problem (again).** If departments raised the evidentiary bar for arrest over time, clearance fell mechanically even as substantive performance held steady. Be cautious about reading detective-staffing-vs-clearance as detective-staffing-vs-effectiveness.

---

## Texas-specific findings

The published Texas-specific literature on homicide clearance is thin. Sam Houston State's College of Criminal Justice has produced the most empirical work on Texas policing, mostly through the CRIMES information-management project, but I did not find a peer-reviewed clearance-rate study focused on Texas cities. The Houston Police Foundation, Greater Houston Partnership, and Justice Innovation Center at the University of Houston Law Center have all touched the topic in gray literature.

What we know from non-academic sources:

- **Houston PD.** Clearance: 52% (2020) → 55% (2021) → 69% (2022). Department credits an expanded homicide division and new technology. The 2022 jump is large enough (and reversible enough — clearance is partial-year for 2022 at the time of reporting) to merit independent verification. **This is your single best Texas natural-experiment candidate.**

- **Dallas PD.** Reported 78% (2020) per DPD; FBI showed 39%. Detective count fell from 28 (2017) to 16 (2018), per CBS Texas reporting; not clear whether it has since recovered. The discrepancy between self-reported and FBI numbers makes Dallas the most measurement-fraught city in the state.

- **Austin PD.** Stopped publishing annual crime reports in 2021. Reported 100% homicide clearance for 2023 (first time since 2005). Department is 250-500 officers under authorized strength, depending on year. Detectives have reportedly been pulled to patrol assignments — a *negative* staffing shock to the homicide unit even as headline clearance rose. Austin is the best example of the case-mix story: clearance can rise because homicides fall and the remaining cases are easier, not because investigation improved.

- **San Antonio PD.** Homicide rate hit a 30-year high in 2022 (195 murders). I did not find a publicly reported clearance rate for SAPD homicide in the 2020-23 period from a primary source. PIA target.

- **Fort Worth.** Reported 72% clearance for 2020 (self-report); FBI showed 55%.

The post-2020 clearance collapse story in Texas is real but uneven. Houston shows a partial recovery; Dallas reports recovery but the data are suspect; Austin reports a remarkable recovery but the underlying staffing situation contradicts the simple "more detectives → more clearance" story; San Antonio is an information void.

**No academic paper I could find has analyzed the 2020-23 Texas clearance trajectory comparatively.** This is itself an opportunity.

---

## Methodological angles Brennan may not have considered

1. **Synthetic control on Houston's 2021-22 homicide unit expansion.** This is the single best identified-shock in the Texas data, has a clean treatment date, and has plausible donor cities (Phoenix, San Diego, Philadelphia, Detroit, Memphis, Indianapolis). The Abadie-Diamond-Hainmueller / Ben-Michael augmented synthetic control framework is now standard and accessible. If Houston really did go 52→69 because of staffing, SCM will pick it up. If it didn't, SCM will tell you that too.

2. **Bunching at reporting thresholds.** Departments may bunch reported clearance just above politically salient thresholds (50%, 60%, the national average). McCrary-style density-discontinuity tests on monthly self-reported clearance figures across TX agencies would flag manipulation, and would be a small standalone paper.

3. **Exceptional-clearance share as a falsification test.** If your detective-FTE coefficient on total clearance is positive but the coefficient on *arrest* clearance (excluding exceptional) is null, you've found a reporting effect, not a real effect. Always run both.

4. **Time-to-clearance as a continuous outcome.** Cox proportional-hazards models on time-from-incident-to-arrest are standard in the literature (Roberts 2007) and give you more statistical power than binary clearance Y/N. The Cook-Braga finding that effort matters mostly *after* 48 hours is directly testable in a hazard-model framework.

5. **The civilian-staff angle.** PIA for civilian crime-analyst FTEs alongside sworn detectives. Boston's reform credited the civilian analysts heavily. If TX departments vary in this ratio, it's a low-cost extension that could differentiate your paper from prior work.

6. **Patrol-officer first-responder protocols as a hidden treatment.** Wellford & Cronin (1999) is unambiguous that patrol-level first response drives clearance. If any TX agency adopted a first-responder protocol change in the period — body-worn camera deployment, in-service training overhaul, sergeant supervision changes — that's a confound but also a separately testable shock.

7. **Don't underestimate the cross-city sample-size problem.** Texas has ~6 large municipal departments worth analyzing (Houston, Dallas, San Antonio, Austin, Fort Worth, El Paso, maybe Arlington). That's a tiny N for cross-sectional inference. Brennan should plan for either (a) within-city year-by-year variation as the main identification, or (b) micro-data at the case level pooled across cities, with city fixed effects.

8. **Pre-register and publish a pre-analysis plan.** This is a politically loaded research question. Pre-registering the model specification, the control variables, and the threshold for "the thesis survives" will dramatically increase the credibility of whatever you find — particularly if the answer is null.

---

## Bibliography

Adamson, J., & Rentschler, L. (2025). "How policing incentives affect crime, measurement, and justice." *Economic Inquiry* 63(2): 545-567. https://onlinelibrary.wiley.com/doi/10.1111/ecin.13270

Bjerk, D. (2022). "Does greater police funding help catch more murderers?" *Journal of Empirical Legal Studies* 19(3): 528-559. https://onlinelibrary.wiley.com/doi/10.1111/jels.12325 — open-access working version at https://static1.squarespace.com/static/5b7ea2794cde7a79e7c00582/t/64740df855cded580bccb3c4/1685327353164/does+greater.pdf

Braga, A. A. (2021). *Improving Police Clearance Rates of Shootings: A Review of the Evidence.* Manhattan Institute. https://manhattan.institute/article/improving-police-clearance-rates-of-shootings-a-review-of-the-evidence

Braga, A. A., & Dusseault, D. (2018). "Can Homicide Detectives Improve Homicide Clearance Rates?" *Crime & Delinquency* 64(3): 283-315. https://journals.sagepub.com/doi/10.1177/0011128716679164

Braga, A. A., Turchan, B. S., & Barao, L. M. (2019). "The Influence of Investigative Resources on Homicide Clearances." *Journal of Quantitative Criminology* 35(2): 285-318. https://link.springer.com/article/10.1007/s10940-018-9386-9

Brookman, F., Maguire, E. R., & Maguire, M. (2019). "What Factors Influence Whether Homicide Cases Are Solved? Insights From Qualitative Research With Detectives in Great Britain and the United States." *Homicide Studies* 23(2): 145-174. https://journals.sagepub.com/doi/10.1177/1088767918793678

Campedelli, G. M. (2024). "Homicides involving Black victims are less likely to be cleared in the United States." *Criminology* 62(3): 587-619. https://onlinelibrary.wiley.com/doi/10.1111/1745-9125.12362

Carter, D. L., & Carter, J. G. — *flagged for verification*. A specific Carter & Carter 2016 publication on cold-case staffing could not be confirmed from open sources. Brennan should treat this citation as unconfirmed and verify before relying on it.

Chalfin, A., & McCrary, J. (2018). "Are U.S. Cities Underpoliced? Theory and Evidence." *Review of Economics and Statistics* 100(1): 167-186.

Cook, P. J., Braga, A. A., Turchan, B. S., & Barao, L. M. (2019). "Why do gun murders have a higher clearance rate than gunshot assaults?" *Criminology & Public Policy* 18(3): 525-551. https://onlinelibrary.wiley.com/doi/10.1111/1745-9133.12451

Cook, P. J., & Lopez, J. (2024). "Explaining the Extraordinary Decline in Chicago's Homicide Arrest Rates, 1965 to 1994 and Beyond: Trends in Case Mix Versus Standards for Arrest." *Journal of Contemporary Criminal Justice* 40(2). https://journals.sagepub.com/doi/full/10.1177/10439862231219470

Cook, P. J., & Mancik, A. (2024). "The Sixty-Year Trajectory of Homicide Clearance Rates: Toward a Better Understanding of the Great Decline." *Annual Review of Criminology* 7: 59-83. https://www.annualreviews.org/content/journals/10.1146/annurev-criminol-022422-122744

Eck, J. E. (1983). *Solving Crimes: The Investigation of Burglary and Robbery.* Police Executive Research Forum.

Eck, J. E. (2019). "The new detective." *Criminology & Public Policy* 18(3): 601-622. https://onlinelibrary.wiley.com/doi/10.1111/1745-9133.12450

Greenwood, P. W., Chaiken, J. M., & Petersilia, J. (1977). *The Criminal Investigation Process.* RAND Corporation / Lexington Books. Reports R-1776 through R-1778, https://www.rand.org/pubs/reports/R1776.html

Hogan, T. P. (2022). "De-prosecution and death: A synthetic control analysis of the impact of de-prosecution on homicides." *Criminology & Public Policy* 21(3). https://onlinelibrary.wiley.com/doi/10.1111/1745-9133.12597

Hsu, K., Emerick, B. K., & Sytsma, V. A. (2024). "Police personnel allocation and homicide clearance." *Policing: An International Journal* 47(5): 786-803. https://www.emerald.com/insight/content/doi/10.1108/pijpsm-08-2023-0100/full/html

Lum, C., Wellford, C., et al. (2021). *Identifying Effective Investigative Practices.* Center for Evidence-Based Crime Policy / NIJ. https://cebcp.org/wp-content/uploads/2021/05/LumWellfordInvestigationsProjectFINAL.pdf

Mancik, A. M., Parker, K. F., & Williams, K. R. (2018). "Neighborhood Context and Homicide Clearance: Estimating the Effects of Collective Efficacy." *Homicide Studies* 22(2): 188-213. https://journals.sagepub.com/doi/10.1177/1088767918755419

Mello, S. (2019). "More COPS, Less Crime." *Journal of Public Economics* 172: 174-200. https://www.princeton.edu/~smello/papers/cops.pdf

Murder Accountability Project. https://www.murderdata.org/

Police Executive Research Forum. (n.d.). *Promising Strategies for Strengthening Homicide Investigations.* https://www.policeforum.org/assets/homicideinvestigations.pdf

Roberts, A. (2007). "Predictors of Homicide Clearance by Arrest: An Event History Analysis of NIBRS Incidents." *Homicide Studies* 11(2): 82-93.

Roberts, A. (2015). "Adjusting Rates of Homicide Clearance by Arrest for Investigation Difficulty: Modeling Incident- and Jurisdictional-Level Obstacles." *Homicide Studies* 19(3): 273-300. https://journals.sagepub.com/doi/10.1177/1088767914536984

Scott, T. L., Wellford, C., Lum, C., & Vovak, H. (2019). "Variability of Crime Clearance Among Police Agencies." *Police Quarterly* 22(1): 82-111.

Wellford, C., & Cronin, J. (1999/2000). *An Analysis of Variables Affecting the Clearance of Homicides: A Multisite Study.* National Institute of Justice. https://www.ojp.gov/library/publications/analysis-variables-affecting-clearance-homicides-multisite-study and summary at https://www.ojp.gov/pdffiles1/jr000243b.pdf

Wellford, C. F., Lum, C., Scott, T., Vovak, H., & Scherer, J. A. (2019). "Clearing Homicides: Role of Organizational, Case, and Investigative Dimensions." *Criminology & Public Policy* 18(3): 553-600. https://onlinelibrary.wiley.com/doi/10.1111/1745-9133.12449

**Trend / data sources (non-academic but useful):**

- Council on Criminal Justice, *Trends in Homicide* series. https://counciloncj.org/homicide-trends-report/
- CBS News / CBS Texas, "Crime Without Punishment" (2023), DFW clearance reporting. https://www.cbsnews.com/texas/news/crime-without-punishment-dallas-forth-worth-homicide-clearance-rate/
- Austin Monitor (2024) on APD's failure to publish clearance data. https://austinmonitor.com/stories/2024/09/why-doesnt-the-austin-police-department-publish-yearly-reports-on-the-crimes-it-solves/
- Right on Crime / Texas Public Policy Foundation (Pressley & Jackson, 2024), *Ensuring Justice: Innovative Approaches to Improve Crime Clearance Rates.* https://rightoncrime.com/wp-content/uploads/2025/01/2024-12-ROC-Crime-Clearance-Rates-PressleyJackson_FINAL.pdf
- City of San Antonio NIBRS open data portal. https://www.sa.gov/Directory/Departments/SAPD/Transparency-Open-Data/Open-Data-Library/NIBRS
- Texas UCR portal. https://txucr.nibrs.com/
