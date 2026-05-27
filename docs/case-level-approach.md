# Case-Level Homicide Disposition: A Methodological Scoping Memo for the Texas Project

Prepared for Brennan Griffin, May 2026.
Scope: Whether to pivot the Texas homicide-clearance project from aggregate (UCR/NIBRS) clearance rates to a bottom-up, case-level dataset built from Texas Public Information Act requests; how to do it defensibly if we proceed; and what the precedent literature and Texas PIA case law say about the practical risks.

This memo presumes familiarity with the May 2026 literature review (`docs/literature-review.md`). Cross-reference for the case-mix dominance finding (Roberts 2015; Campedelli 2024; Mancik et al. 2018) and the Dallas self-report vs. FBI discrepancy that motivated the pivot.

---

## TL;DR

- The case-level PIA approach is methodologically sound *and* there are two strong precedents (Washington Post 2018; The Trace + BuzzFeed News 2019) for executing it at multi-city scale. Both built standardized homicide-disposition datasets from FOIA/PIA pulls across 22-50 large U.S. cities, and both made their code and data public.
- The Texas PIA gives us a workable but messy path. The *Houston Chronicle Publishing Co. v. City of Houston*, 531 S.W.2d 177 (Tex. Civ. App. 1975) line of cases — codified into §552.108(c) — guarantees release of "basic information" (offense, location, time, victim identification, investigating officers) even on uncleared cases. The hard part is getting *disposition status* (cleared by arrest / cleared by exception / open) on still-open cases, where §552.108(a)(1) lets the agency stall.
- Survival-curve evidence supports the 2023 vintage: 50% of cleared cases clear within one week, ~93% within one year (Wellford & Cronin 1999/2000). By a 2026-Q3 pull, a 2023-vintage case has had ~2.5-3.5 years to clear, which captures essentially the entire mass of cases that will ever clear. The marginal gain from waiting for 2022 is small; the cost in topical staleness is real.
- Cost is the biggest unknown but bounded. Texas's statutory $15/hour labor charge plus $0.10/page (1 TAC §70.3) is the legal cap. A 15-city, 1,000-1,500-record pull is probably $3,000-$12,000 in PIA fees plus 200-400 hours of cleaning. The single largest unbudgeted risk is the 60-business-day AG-ruling delay each time an agency invokes §552.108 — that lag, not money, is the binding constraint.
- The single biggest methodological risk is **selection on disposition**: cases an agency declines to release (open / under investigation / pending) are also the cases least likely to have cleared, so an analyst who treats refusal as missing-at-random will overstate clearance. The fix is to code "responsive but withheld under §552.108(a)(1)" as its own category and treat it as a strong probabilistic signal of non-clearance.

---

## The Washington Post precedent: "Where killings go unsolved" (2018)

The reporting project was authored by Wesley Lowery, Steven Rich, Kimbriell Kelly, and Ted Mellnik; it was a 2019 Pulitzer finalist for national reporting. They FOIA'd ~52,000 criminal homicides over the decade 2007-2017 (NYC was a partial outlier with only two years of data) across **50 of the largest U.S. cities** and published the standardized dataset at [washingtonpost/data-homicides on GitHub](https://github.com/washingtonpost/data-homicides) under CC BY 4.0 / MIT licenses for code.

**Field schema** (verbatim from the published CSV):
`uid, reported_date, victim_last, victim_first, victim_race, victim_age, victim_sex, city, state, lat, lon, disposition`

That's a notably *thin* schema by case-mix standards. Critically, what they got was: incident date, victim demographics, geolocation, and a disposition code (closed by arrest / closed without arrest / open). They did **not** systematically capture weapon, victim-offender relationship, location-type (indoor/outdoor), motive, time-to-clearance, or clearance mechanism (arrest vs. exception). For our purposes that's a ceiling we'd want to beat.

**City coverage and Texas representation.** The README does not enumerate the cities. From third-party catalogs and the dataset itself, Texas representation in the WaPo file is limited — Dallas appears (referenced in the mass-shooting exclusion footnote), but Houston, Austin, San Antonio, and Fort Worth are not all in the published 50-city core. Confirm by pulling the unique values of `city` from the CSV before relying on any specific TX coverage. The dataset's effective end date is mid-2017 for most cities, which means it is now *eight years stale* for any specific Texas reform you'd want to study.

**Methodological choices worth borrowing.** Reporters received data "in many formats, including paper," and spent months cleaning and reconciling. Where departments provided partial information, they triangulated with death certificates, court records, and medical examiner reports. They explicitly compared their homicide counts and aggregate closure rates against FBI/UCR to validate. **The triangulation pattern is the model for us**: PIA the police department, cross-check against the medical examiner / county clerk death records, and cross-check the count against TXUCR / FBI CDE.

**What it isn't.** The WaPo data are essentially a binary outcome with geolocation. They support spatial-cluster analysis of unsolved cases (their published "unsolved zones" maps) but not investigation-effort modeling. There is no case-effort variable, no investigative-action variable, no time-to-clearance. That is what we would need to add.

**Subsequent academic use.** The dataset has been used in dozens of papers, methods classes (it's the basis for a P8105 Columbia biostatistics homework), and at least one peer-reviewed extension — Pittsburgh public-health and Indianapolis epidemiology groups have built on it. None of those is a Texas-specific replication.

A useful peer project: **The Trace + BuzzFeed News (2019)**, "Shoot Someone in a Major U.S. City, and Odds Are You'll Get Away With It," published the [`local-police-data-analysis`](https://github.com/the-trace-and-buzzfeed-news/local-police-data-analysis) repo. They PIA'd 22 municipal departments for case-level data on homicides, aggravated assaults, and nonfatal shootings, with explicit fields for **victim and suspect names, demographics, weapon, case status, location, and motive** — a thicker schema than WaPo's. Their published [methodology document](https://www.documentcloud.org/documents/5692688-Methodology-for-Local-Police-Data.html) is the most directly useful template for what we'd ask for. They also confronted Brennan's exact selection problem — many departments refused, several gave only partial fields — and were transparent about it in the methodology.

---

## Academic case-level work and what it added over aggregate research

**Wellford, Lum, Scott, Vovak & Scherer (2019), "Clearing Homicides," *Criminology & Public Policy* 18(3): 553-600.** The most direct methodological cousin to what Brennan is contemplating. Funded by the Laura and John Arnold Foundation. They reviewed **detailed case files** from 50 agencies across 30 cities, building a case-level dataset with investigative-action variables (search warrants executed, DNA tested, witnesses re-interviewed, etc.) that no aggregate panel could capture. What they got that aggregate work missed: which *specific* investigative behaviors predict clearance net of case mix, and which *organizational* properties (analyst-to-detective ratio, peer review, supervision intensity) magnify investigative effort.

**Braga, Turchan & Barao (2019), "The Influence of Investigative Resources on Homicide Clearances," *JQC* 35(2): 285-318**, and the companion **Cook, Braga, Turchan & Barao (2019)** paper in *C&PP* 18(3): 525-551. Boston PD partnership data on 465 homicides 2007-2014. Case-level investigative-action coding allowed them to show that homicide and nonfatal-shooting clearance are identical in the first 48 hours (both ~11%), and the 24-point gap that develops thereafter is entirely attributable to *sustained investigative effort on homicides*. That finding is invisible in any aggregate clearance series.

**Roberts (2007), "Predictors of Homicide Clearance by Arrest: An Event History Analysis of NIBRS Incidents," *Homicide Studies* 11(2): 82-93**, and **Roberts (2015)**, *Homicide Studies* 19(3): 273-300. Roberts used NIBRS case-level extracts (national, but with substantial agency-non-reporting gaps) and Cox proportional-hazards models to estimate the time-to-clearance hazard rate, conditional on case characteristics. This is the closest published precedent for the *survival analysis* we should run on the Texas data.

**Pastia, Davies & Wu (2017), "Factors Influencing the Probability of Clearance and Time to Clearance of Canadian Homicide Cases, 1991-2011," *Homicide Studies* 21(3): 199-223.** Kaplan-Meier survival analysis plus Cox regression on 11,297 Canadian homicides. The Canadian *Homicide Survey* gives them a complete national case-level census Texas can't match, but the analytical pattern is directly portable.

**McEwen (2009), *Research Analysis of the Phoenix Homicide Clearance Project*, NIJ Report 244481.** Two-year study period at Phoenix PD; closed-file qualitative coding of both cleared and uncleared cases. The project was *not* successful at moving the headline clearance rate, but the case-file work showed that targeted interventions improved clearance on hard cases. Useful as a cautionary tale on what a single-city case-level study can and can't show.

**Cook & Mancik (2024) and Cook & Lopez (2024)**, both reviewed in the prior literature memo: they relied on case-level Chicago data (1965-onward) to make the "rising arrest standard" argument. Aggregate data cannot distinguish "fewer arrests because investigations failed" from "fewer arrests because prosecutors raised the evidentiary bar." Case-level prosecutor-disposition data can.

**Net of all this:** case-level data routinely lets researchers separate (a) what investigators *did*, (b) what *case characteristics* faced them, and (c) what *organizational and prosecutorial choices* were operating in the background. Aggregate clearance rates collapse all three into one number. For Brennan's specific question — does detective FTE per case actually move clearance, net of case mix — the case-level approach is not merely defensible, it's *required*.

---

## Time-to-clearance survival curve: defending the 2023 vintage

The single most-cited empirical anchor on the survival curve is Wellford & Cronin (1999/2000), [*An Analysis of Variables Affecting the Clearance of Homicides: A Multisite Study*](https://www.ojp.gov/pdffiles1/jr000243b.pdf), NIJ. In their four-city sample (798 homicides, 1994-95):

| Time since incident | Cumulative % of cleared cases cleared by then |
|---|---|
| Within 1 week | ~50% |
| Within 1 month | ~75% (interpolated from the curve) |
| Within 1 year | 93.2% |
| Within 3 years | approaches 100% |

That implies, conservatively, **<7% of cases that will *ever* clear take longer than one year to do so.** Of those, the vast majority are within the second year; the tail beyond three years is dominated by cold-case DNA / genealogy hits, which are rare in absolute number.

Pastia, Davies & Wu (2017) is slightly less optimistic: in Canadian data, "most cleared cases are solved within a week, whereas 25% are resolved within a year." That phrasing implies a heavier right tail than Wellford-Cronin, but their cohort spans 20 years and includes cold-case re-investigations under different organizational regimes.

**Implication for vintage choice.** A 2023 case PIA'd in mid-to-late 2026 has had ~30-42 months of clearance opportunity. By Wellford-Cronin that captures >95% of the ultimate clearances. By the more conservative Canadian estimate, we'd capture ~90%. Either way, the *marginal* gain from waiting and pulling 2022 (which would add another year of right-censoring resolution) is small — maybe 2-3 percentage points more cases settled. The cost is two extra years of staleness and a less politically resonant publication date.

**Recommendation:** stick with 2023. But explicitly model the right-censoring rather than ignore it. For any case still coded "open" at PIA-response date, run the Kaplan-Meier with that case censored at response date; do *not* impute it as "uncleared." This is exactly the design Roberts (2007) and Pastia et al. (2017) used and is standard in the literature. If we want a sensitivity check, pull a small parallel sample of 2021 cases (300 records, 3-4 cities) and see whether the additional 24 months of follow-up materially changes the estimated clearance hazard. If the 2021 cohort's 24-36-month tail is empirically small, that's a published-ready robustness check.

---

## Texas PIA navigation: §552.108 and the *Houston Chronicle* doctrine

The governing statute is **Texas Government Code §552.108**, "Exception: Certain Law Enforcement, Corrections, and Prosecutorial Information." Three subsections matter for our purposes:

- **§552.108(a)(1)** — agencies may withhold information about pending / unconcluded investigations if release would interfere with detection, investigation, or prosecution. This is the open-case exemption.
- **§552.108(a)(2)** — agencies may withhold information about investigations that concluded in something other than conviction or deferred adjudication. This is the *closed-no-conviction* exemption. **For our project, this is the more troublesome one**: a case "cleared by exception" (offender dead, prosecuted elsewhere, victim refusal to cooperate) ends without conviction, so the agency can lawfully refuse to release the case file.
- **§552.108(c)** — neither (a)(1) nor (a)(2) excepts **"basic information about an arrested person, an arrest, or a crime."** The statute requires *prompt* release of basic information.

What counts as "basic information" was settled in **Houston Chronicle Publishing Co. v. City of Houston**, 531 S.W.2d 177 (Tex. Civ. App.-Houston [14th Dist.] 1975), petition refused, n.r.e. The court held that the following must be released on constitutional First Amendment grounds even independent of the Open Records Act:

> the offense committed, location of the crime, identification and description of the complainant, the premises involved, time of occurrence, description of the weather, a detailed description of the offense, and the names of the arresting and investigating officers.

Plus, on arrest, the name/age/address/race/sex/occupation/alias/physical condition of the arrested person; the date and time of arrest; the offense charged; details of the arrest; booking information; release/transfer notation; and bonding information.

This is the foundation. Every Texas PIA officer is trained on *Houston Chronicle* and ORD-127 (1976). They *cannot* refuse those fields under §552.108. The Texas AG handbook explicitly reiterates that "basic information shall be promptly released." This is your floor.

**The recent §552.108(d) deceased-victim amendment** (codified out of HB 30 / 88th Leg.) further holds that the law-enforcement exception does not apply to records "if a person described by or depicted in the information is deceased or incapacitated and each other person described in the information consents." Homicide victims are by definition deceased — that subsection is relevant if any agency tries to deny on the victim-privacy theory.

**The 60-day AG-ruling delay is the real cost.** Per Houston PD's own published [PIA practice](https://www.houstontx.gov/police/public_information.htm): "If the case was not closed by conviction and you submit an Open Records request for the whole report, your request will be forwarded to the Texas Attorney General's Office for a ruling, a process which takes around 60 business days." That's three calendar months *per request* if the agency invokes the exception. For a 15-city pull this could add a year of cumulative lag if we're not careful about how we sequence and structure requests. **Mitigation: explicitly request only the basic-information fields (citing *Houston Chronicle* and §552.108(c)) in the first wave; defer the full case file to a second wave only for cases of analytic interest.**

I could not find a specific ORD or AG letter ruling that addresses the precise question of bulk homicide-disposition pulls for completed-year analytics. The closest relevant material is OR201205190, OR201101795, and the 2023 OR202303690 (Paxton-era) letter rulings, which apply §552.108 case-by-case rather than establishing categorical doctrine. Worth a focused Westlaw / AG-database search before drafting the final request template.

---

## Universe identification: which homicides to PIA

To PIA "every 2023 homicide in city X" requires first knowing the universe. Options, with tradeoffs:

| Source | Strengths | Weaknesses |
|---|---|---|
| **FBI Crime Data Explorer / NIBRS 2023 extract** | Standardized national format; case-level by 2023; freely downloadable | Texas agencies reported unevenly through the SRS→NIBRS transition; ~19% of 2022 U.S. homicides were never reported to FBI per CDC/FBI comparison; some TX agencies still missing fields |
| **SHR (Supplementary Homicide Report) via MAP** | MAP supplements with FOIA-obtained records for non-reporting agencies; CSV-ready | Same SRS-to-NIBRS transition gap; victim/offender demographic fields good, but no disposition lag tracking |
| **TXUCR / Crime in Texas annual report (DPS)** | Texas-specific, covers all TX agencies, includes 2023 | Aggregate-level reporting in the published PDF; case-level access requires separate request to DPS; some agencies revise prior-year numbers |
| **City open-data portals** | San Antonio publishes NIBRS-format data directly; Houston publishes monthly crime by beat; Dallas publishes a real-time incident-level open data feed | Inconsistent across cities; field schemas differ; some don't include disposition |
| **Medical examiner / coroner records** | County-level (Harris, Dallas, Bexar, Travis, Tarrant), categorical "homicide" cause of death; independent of police | County not city boundary; includes deaths later ruled non-criminal; PIA request to ME's office is separate workflow |
| **News scrapers / local trackers** | ABC13 / H-Town Society / *Dallas Morning News* maintain near-real-time homicide trackers in DFW and Houston; granular individual victim coverage | Coverage thinner in San Antonio, Austin, Fort Worth, El Paso; not centralized; coding inconsistencies |
| **PIA the universe directly** | The agency's own homicide-unit case log is the gold standard for what they consider a homicide | Adds another PIA round; agencies vary in how they define "homicide" vs. "death investigation" vs. "criminal homicide" |

**Recommended approach:** Triangulate. Use TXUCR + FBI CDE as the per-city expected count anchor. PIA each agency's homicide-unit *case log* as step zero (one-line-per-case: incident number, date, location, victim name, status). That gives you the universe. *Then* PIA the case-level details for each case in wave two. Cross-validate the case-log count against ME records and news-tracker counts; investigate any city whose three numbers disagree by more than ~5%.

The Murder Accountability Project is a worth-keeping-in-mind side reference: they obtained ~27,000 homicides through FOIA that local police never reported to the FBI, demonstrating that the SHR/NIBRS undercount is non-trivial. Pull their TX state file as a cross-check on the universe.

---

## Cost and effort: a 15-city, 2023-vintage pull

**Statutory cap (1 Tex. Admin. Code §70.3 and §70.4):**

- Standard-size paper copies: $0.10/page
- Personnel labor: **$15/hour**, billable only for requests >50 pages or located in multiple buildings
- 20% overhead surcharge on labor
- Electronic-media charge: minimal (per actual cost of media)
- Cost estimate required if total will exceed **$40**
- §552.275 lets agencies set "reasonable limits" on time spent per requestor (typically 36 hours / year before they can refuse further free work)

**Houston PD's published practice:** copy of a single offense report = **$6 in person, $6 by mail with money order**. That's a useful per-record anchor for a redacted "front-of-report" basic-information pull.

**Indicative scale.** 15 TX cities, 2023 homicide counts roughly: Houston ~270-350, Dallas ~245, San Antonio ~155, Austin ~70, Fort Worth ~75-95, El Paso ~35, Arlington ~30, Plano ~10, Garland ~15, Irving ~15, Laredo ~25, Lubbock ~40, Corpus Christi ~30, Amarillo ~30, Brownsville ~10. Total **≈ 1,050-1,300 records**. Bulk pull at $6/record is **$6,300-$7,800** in copy fees as a ceiling; in practice many agencies will fulfill electronically at near-zero per-record cost. Labor charges might add another $1,500-$3,000 for compilation and review. Realistic total: **$8,000-$12,000** in agency-billed fees if every agency charges to the cap; **$3,000-$5,000** if most produce electronically.

The dominant cost is *not money* — it's analyst hours. The WaPo project consumed reporter-months of cleaning and triangulating data that arrived "in many formats, including paper." The Trace + BuzzFeed effort similarly required building per-department parsers. Budget **200-400 hours of structured data cleaning** for a 1,000-record multi-city pull. At Texas Appleseed-equivalent fully-loaded rates that's $15,000-$30,000 in staff time, which dwarfs the PIA fees.

The 60-business-day AG-review delay is the binding scheduling constraint. To deliver a clean 2023 dataset by, say, Q1 2027, the first wave of basic-information requests would need to go out by Q3 2026, with second-wave full-file requests by Q1 2027 for any AG-pending cases.

---

## Risks and open questions

1. **Selection on disposition (the biggest risk).** Agencies will produce records most readily for cases that closed with a clean arrest and conviction. They will stall, redact, or partially produce on open cases (§552.108(a)(1)) *and* on cases cleared-by-exception without conviction (§552.108(a)(2)). Treating those refusals as missing-at-random will systematically overstate clearance. The required design fix: code refusal-reasons as their own categorical outcome, model them probabilistically, and validate the resulting clearance estimate against the agency's UCR-reported clearance for the same year. If the bottom-up estimate diverges sharply from UCR, that gap is itself a finding.

2. **Inter-agency definition variance.** What counts as a "homicide" varies. Some agencies count justifiable homicides (police shootings) in the case log; some don't. Some count vehicular manslaughter; some don't. Some count "death investigations" that may later be ruled accidental. The case-log PIA at step zero should explicitly request the agency's *operational definition* and ask for all death investigations coded as criminal homicide, then filter analytically.

3. **Clearance-by-exception coding inconsistency.** The literature (and our prior memo) flags this as a major problem in aggregate data. At the case level we can ask each agency for the specific exception-reason coding per UCR Handbook (death of offender / prosecution denied / extradition denied / victim refusal / juvenile). But agency adherence to those codes varies. Triangulating against court / DA records would catch the worst inconsistencies.

4. **The mid-sized-city problem.** For cities with 10-30 homicides per year, even a complete pull yields too few cases for within-city statistical inference. The case-level data will only be powerful pooled across cities with city fixed effects.

5. **Reverse causality on the original research question.** Even with perfect case-level data, the detective-FTE-vs-clearance question retains the endogeneity problem flagged in the prior memo (Bjerk 2022): cities allocate detectives in response to homicide trends. Case-level data improves the *outcome side* but doesn't solve the *treatment side*. The natural-experiment strategies (Houston 2021-22 expansion synthetic control; Dallas 2017-18 detective collapse DiD) remain the credible identification path.

6. **Publication / political risk.** Case-level disposition data are sensitive. Some agencies will not respond to bulk requests by an advocacy-org affiliate; others will respond more slowly than to journalistic requesters. Pre-coordinating with a Texas-based investigative journalism partner (Texas Tribune, Houston Landing, Dallas Morning News) could materially accelerate fulfillment.

7. **Unverified assumption: 2023 detective-staffing data exists at the case-level.** Detective assignment per case is sometimes captured in police records management systems and sometimes not. If agencies cannot or will not produce "lead detective ID per case," the most valuable variable for our specific research question never arrives. **Worth one or two pre-pilot phone calls to PD records officers to test this before committing to the full 15-city pull.**

8. **One legal point to verify before drafting templates.** I could not confirm an AG letter ruling that explicitly addresses bulk completed-year homicide pulls under §552.108(c). Worth a focused search of the Open Records Letter Rulings database (texasattorneygeneral.gov) and *if* nothing is on point, that's actually useful — it means agencies will likely process our requests case-by-case under §552.108(c), which gives us the *Houston Chronicle* basic-information fields by default.

---

## Recommended next steps (if Brennan greenlights)

1. **Pre-pilot:** Pick 2 cities (Austin + Fort Worth, say — small enough to be tractable, different enough to be informative). PIA each for (a) the 2023 homicide case log; (b) for 10 closed cases each, the full basic-information record. Time the responses. Inventory which fields actually arrive. This validates the cost/effort estimate before committing.
2. **Draft a model PIA letter** that cites *Houston Chronicle*, §552.108(c), and the §552.108(d) deceased-person amendment. Have it reviewed by a Texas PIA attorney (FOIFT can refer pro-bono counsel).
3. **Decide the schema before pulling.** Pre-commit to which fields we'll attempt to capture and which we'll treat as out-of-scope. The Trace + BuzzFeed schema is a defensible starting template.
4. **Coordinate with at least one news partner.** Their PIA-fulfillment leverage exceeds Texas Appleseed's, and joint publication amplifies impact.
5. **Pre-register the analysis plan.** Given the political stakes (questioning self-reported clearance rates challenges police narratives), pre-registration on OSF before the data arrive will dramatically strengthen any downstream findings — particularly null findings.

---

## Bibliography (case-level approach additions)

Braga, A. A., Turchan, B. S., & Barao, L. M. (2019). "The Influence of Investigative Resources on Homicide Clearances." *Journal of Quantitative Criminology* 35(2): 285-318. https://link.springer.com/article/10.1007/s10940-018-9386-9

Cook, P. J., Braga, A. A., Turchan, B. S., & Barao, L. M. (2019). "Why do gun murders have a higher clearance rate than gunshot assaults?" *Criminology & Public Policy* 18(3): 525-551.

Houston Chronicle Publishing Co. v. City of Houston, 531 S.W.2d 177 (Tex. Civ. App.-Houston [14th Dist.] 1975, writ ref'd n.r.e.). https://law.justia.com/cases/texas/supreme-court/1976/b-5773-0.html

McEwen, T. (2009). *Research Analysis of the Phoenix Homicide Clearance Project*, NIJ Report 244481. https://www.ojp.gov/pdffiles1/nij/grants/244481.pdf

Murder Accountability Project. *Data & Docs*. https://www.murderdata.org/p/data-docs.html

National Case Closed Project. *Core Standards for Fatal and Non-fatal Shooting Investigations*. https://nationalcaseclosed.org/products/docs/Core-Standards-for-Fatal-and-Non-fatal-Shooting-Investigations.pdf

Pastia, C., Davies, G., & Wu, E. (2017). "Factors Influencing the Probability of Clearance and Time to Clearance of Canadian Homicide Cases, 1991-2011." *Homicide Studies* 21(3): 199-223. https://journals.sagepub.com/doi/10.1177/1088767916686148

Roberts, A. (2007). "Predictors of Homicide Clearance by Arrest: An Event History Analysis of NIBRS Incidents." *Homicide Studies* 11(2): 82-93.

Roberts, A. (2015). "Adjusting Rates of Homicide Clearance by Arrest for Investigation Difficulty." *Homicide Studies* 19(3): 273-300.

Texas Attorney General. *Public Information Act Handbook 2024*. https://www.texasattorneygeneral.gov/sites/default/files/files/divisions/open-government/publicinfo_hb.pdf

Texas Government Code, Chapter 552. https://statutes.capitol.texas.gov/Docs/GV/htm/GV.552.htm

Texas Administrative Code, Title 1, §70.3. *Charges for Providing Copies of Public Information.* https://www.law.cornell.edu/regulations/texas/1-Tex-Admin-Code-SS-70-3

The Trace and BuzzFeed News. (2019). *Local Police Data Analysis* repository and methodology. https://github.com/the-trace-and-buzzfeed-news/local-police-data-analysis and https://www.thetrace.org/violent-crime-data/

Washington Post. (2018). *Murder With Impunity / Where killings go unsolved.* Project page: https://www.washingtonpost.com/graphics/2018/investigations/where-murders-go-unsolved/ and dataset https://github.com/washingtonpost/data-homicides

Wellford, C., & Cronin, J. (1999/2000). *An Analysis of Variables Affecting the Clearance of Homicides: A Multisite Study.* National Institute of Justice. Summary at https://www.ojp.gov/pdffiles1/jr000243b.pdf

Wellford, C. F., Lum, C., Scott, T., Vovak, H., & Scherer, J. A. (2019). "Clearing Homicides: Role of Organizational, Case, and Investigative Dimensions." *Criminology & Public Policy* 18(3): 553-600. https://onlinelibrary.wiley.com/doi/10.1111/1745-9133.12449

---

**Items flagged as uncertain and worth verification:**

- Specific Texas-city coverage in the WaPo 2018 dataset. The README does not enumerate the 50 cities; confirm by inspecting the CSV's `city` column directly. Sampled snapshots suggest the dataset is Albuquerque- and Atlanta-heavy in its sortable opening rows, but that's not evidence of the full universe — the file is ~52,000 rows.
- The specific 22 cities in The Trace + BuzzFeed dataset are listed in their methodology PDF but I did not extract them directly; do so before relying on TX representation.
- The exact Wellford-Cronin 30-day clearance percentage (~75% above) is interpolated from the cited curve, not pulled from the original table. Confirm against the NIJ report PDF before quoting in any publication.
- No specific AG open-records ruling on bulk completed-year homicide pulls was located. The §552.108(c) basic-information framework is well-established, but a targeted ORD search before drafting the template is prudent.
