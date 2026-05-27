# Texas Homicide Detective Units: Descriptive Landscape for Cities With >20 Homicides in 2022

Prepared for Brennan Griffin, May 2026.
Companion to `docs/literature-review.md`, `docs/case-level-approach.md`, and `docs/identification-strategy.md`. Read those first.

Scope: Identify every Texas city that reported more than 20 homicides in 2022, and document — from public sources only — how each city's detective unit responsible for homicides is organized. This is a descriptive scoping memo to support the project's threshold question: is a "homicides per detective" ratio even meaningful, given how much the *scope* of the homicide function varies across departments?

Reference data table: `configs/2022_tx_homicide_universe.csv`.

---

## TL;DR

- **Nine TX cities cross the >20-homicide threshold in 2022 using the FBI/UCR-reported count** (Houston, San Antonio, Dallas, Fort Worth, Austin, Corpus Christi, Lubbock, Amarillo, El Paso). Killeen sits at 19 per FBI / 22 per local reporting and is flagged as a borderline case worth treating as a tenth city for design purposes.
- **There is real organizational heterogeneity even in this small universe.** Five of the nine are dedicated HOM-only squads (Houston, Dallas, Fort Worth, Austin, Amarillo). Two are combined HOM + aggravated-assault units (San Antonio, El Paso). One is a Robbery/Homicide combined unit (Corpus Christi). One is a multi-agency task force (Lubbock's MSCU). No city in the universe uses a "general-assignment" rotation for homicides.
- **The combined-unit cities are not small.** SAPD and EPPD together account for ~255 of the universe's homicides (~32% of the >20 group's 2022 total of ~1,160). Treating their detective FTEs as exclusively-homicide FTEs would *materially* overstate per-case capacity.
- **Public detective-headcount data is mostly stale or absent.** Only Austin (16 detectives + 2 sergeants, plus 7 + 1 cold-case as of 2024) and Fort Worth (14 detectives as of 2024 per WFAA) have credible recent numbers on the public web. El Paso's "15 detectives" figure is from a 2011 Police1.com article and should not be relied on without re-verification. Houston, Dallas, San Antonio, Amarillo, Corpus Christi, Lubbock, and Killeen are all PIA targets for current headcount.
- **The literature review's assumption about Houston was correct in direction but needs verification on the post-2021 squad assignments.** HPD's Homicide Division is dedicated at the public-facing level (Squads, Cold Case, Gang, Investigative Support, SIU). But the March 2021 absorption of ~20 property-crime detectives into Homicide raises the question of whether they were re-assigned to homicide squads, to support, or to a different case-mix. The HPD public-facing org page does not disclose squad-level headcount.

---

## The universe: TX cities >20 homicides in 2022

Using FBI/UCR data (via the city-data.com city pages, which are direct mirrors of FBI Annual Crime in the United States Table 8 / Crime Data Explorer city extracts) the cities clearing the >20 threshold are:

| Rank | City | 2022 homicides (FBI) | 2022 homicides (local report) | Discrepancy notes |
|---|---|---|---|---|
| 1 | Houston | 437 | 434-435 (HPD self-report) | Trivial; HPD and FBI essentially aligned for 2022 |
| 2 | San Antonio | 233 | 230-231 (SAPD); 195 was an earlier mid-year press figure | 2022 inflated by the 53-victim Quintana Road tractor-trailer migrant-smuggling case — *one incident*, 53 deaths, all coded as homicides |
| 3 | Dallas | 212 | 214 victims / 207 incidents (DPD via WFAA, Jan 2023) | Trivial discrepancy on the count itself, but the literature-review memo flags a 39-point gap between DPD self-reported *clearance* and FBI clearance for 2020 |
| 4 | Fort Worth | 101 | 100 (FWPD self-report) | Trivial |
| 5 | Austin | 65 | Combined 142 for 2021+2022 per NICJR/KVUE; APD stopped publishing annual crime reports in 2021 so no audit possible | Cannot cross-check |
| 6 | Corpus Christi | 41 | 41-44 (Caller-Times / local reporting) | Trivial |
| 7 | Lubbock | 26 | 31-34 (KTTZ, areavibes) | Local sources likely include manslaughter and possibly non-criminal homicide investigations counted as "homicides" in press |
| 8 | Amarillo | 23 | 28-30 (thebullamarillo.com) | Same pattern as Lubbock — local press counts run materially higher than FBI; likely manslaughter / justifiable homicide inclusion |
| 9 | El Paso | 22 | 23 (KTSM citing EPPD) | Trivial |

**Borderline (worth flagging for inclusion):**

- **Killeen: 19 per FBI / 22 per Killeen Daily Herald** — this is exactly the kind of FBI-vs-local-press gap the literature review flagged. The KDH report ("Killeen had 22 homicides in 2022; half of them have been solved") draws on KPD's own count. For purposes of unit-organization mapping, Killeen should be carried in the universe.
- **Wichita Falls: 18 per FBI / 18 also per local press** — clearly below threshold even using the lenient count, though the local press *labels* 16 of those 18 as "murders" and the other two as a manslaughter and an officer-involved shooting.
- **Beaumont: 18 per FBI**, locally framed as a year of "violent crimes down ~21%" with no separate murder count contested. Below threshold.
- **Arlington: 16 per FBI** — clearly below threshold. (The prior assumption in CLAUDE.md that Arlington was an "obvious" PIA target may need revisiting on volume grounds even if the city's >250K HB 1900 status remains analytically relevant.)
- **Pasadena: 11 per FBI** — well below threshold.
- **Garland: 5 per FBI** — well below threshold.

Pasadena, Garland, Mesquite, Waco (14 per FBI), Laredo (9 cases / 12 victims per Laredo PD self-report), McAllen (5), and Tyler (11) all fall well short of 20 in 2022 and are not in scope for this memo. They remain candidate "control" cities for any RD-around-250K-population design (per `docs/identification-strategy.md` §3.A1) because most of them sit below the HB 1900 cutoff or with low homicide volume that would make per-detective ratios noisy.

**Universe total**: ~1,159 homicides across nine cities (~1,178 including Killeen), out of ~2,300 homicides statewide in 2022 per the Crime in Texas 2022 annual report citation (clearance percentage statewide was 47.94% — figure I could not independently verify from the original PDF, which I was unable to parse).

## Methodology

1. **Universe identification.** I anchored the FBI/UCR count via city-data.com's per-city tables, which expose the FBI Table 8 / Crime Data Explorer values directly. I cross-checked each FBI number against the closest available local-press or department-self-report value. Where they diverge, I show both and flag the source of the divergence. This handles the documented "self-report vs. FBI" problem (Dallas 2020 = 78% vs. 39%) at the *count* level, not just the clearance level.
2. **Jurisdiction definition.** "City" = the municipal police department of the named city. County sheriffs (Harris CSO, Bexar CSO, etc.) are NOT in this universe because the project's research question is about *municipal* detective allocation. Same for university and transit PDs (UT-Austin PD, METRO PD), which file separately to UCR but had no city in this universe driven into the >20 cohort by their separate filings. **For Lubbock specifically**, the LPD homicide investigative function is bundled into a multi-agency Metropolitan Special Crimes Unit — I treat this as a single LPD-anchored unit for the table but flag it as a non-standard structure.
3. **Unit organization.** For each city I pulled the department's public-facing organizational page, supplemented with news reporting (WFAA on Fort Worth; KCBD on Lubbock; Click2Houston and ABC13 on Houston; KSAT and San Antonio Report on SAPD), and where available the department's posted organizational chart PDF. I made no inferences about scope or staffing that the department's own materials did not support. Where I could not get a primary or near-primary source, I coded the cell as UNKNOWN.
4. **Scope code.** Each city's homicide-handling unit was placed in one of six categories: HOM-only, HOM + nonfatal shootings, HOM + aggravated assault, HOM + robbery, Major Crimes / Crimes Against Persons catch-all, or General-assignment. None of the nine universe cities was coded General-assignment — homicide is a specialized function in all of them. I added an implicit seventh code, *multi-agency task force*, to capture Lubbock's MSCU.
5. **Confidence.** HIGH = official org chart or department page directly states the scope; multiple sources align. MEDIUM = single department-page source. LOW = inferred from third-party reporting only or relying on dated sources.

---

## City-by-city profiles

### Houston — HOM-only at the squad level; PIA needed on post-2021 squad composition

HPD's Homicide Division (Captain S. Q. Zia, per HPD command overview reporting) is structurally dedicated: the public page lists Homicide Squads (the 24/7 case-investigating units), a Cold Case Squad, a Gang Squad (gang-related homicides; FBI Multi-Agency Gang Task Force liaison), Investigative Support (utility/credit/database lookups), and a Special Investigations Unit (officer-involved shootings and internal allegations). The Robbery Division and Major Offenders Division are *separate* HPD divisions; robbery, theft from person, and career-offender cases do not route through Homicide.

The literature-review memo flagged the March 2021 transfer of ~20 property-crime detectives into Homicide (ABC13, 2021). The HPD Homicide page as of 2024 does not enumerate squad-level headcount, so the post-2021 squad assignments — were the property-crime transferees folded into the on-call Homicide Squads, into Investigative Support, or into the Cold Case Squad? — cannot be confirmed without PIA. This is the single most important PIA gap for the project's Houston synthetic-control design (`docs/identification-strategy.md` §A2), because the SCM "first stage" assumption is that 2021-2022 *substantively expanded homicide investigation capacity*, not just shuffled bodies.

Confidence: HIGH on the scope coding (HOM-only); MEDIUM on the post-2021 capacity story until PIA.

### San Antonio — HOM + Aggravated Assault as a single division (the strongest combined-unit case in the universe)

SAPD's investigative organization shows a division literally named "Homicide & Assault" — that's the department's own label, on the official SAPD divisions page. The division "handles crimes involving assault, murder, suicide, overdose and other deaths." Robbery and Sex Crimes are separate units within the larger Investigations Division. SAPD also maintains a public Cold Cases page (a separate program from the operational Homicide & Assault unit, though I could not confirm whether cold-case work is staffed by Homicide & Assault detectives or by a separate sub-unit).

The 2022 count of 233 is materially inflated by a single event: the Quintana Road tractor-trailer migrant-smuggling case (June 2022), in which 53 migrants were found dead in a truck on the southwest side. All 53 deaths are coded as homicides. For any per-detective-workload calculation, this is a once-in-a-generation mass-casualty event being divided by a roughly steady-state detective complement — the per-detective workload number for SAPD 2022 will look anomalous unless the mass event is broken out or excluded.

Publicly available detective and sergeant counts inside the Homicide & Assault division: **none located**. PIA is the only way to get them. The SAPD General Manual Procedure 302 (the organizational policy document hosted on the San Antonio Criminal Defense Lawyers Association website) appears to enumerate the units, but the PDF is a scanned image and not extractable from the public URL I attempted.

Confidence: HIGH on the scope coding (HOM + aggravated assault) because SAPD's own division name confirms it; LOW on staffing.

### Dallas — HOM-only at the squad level, within a CAPERS division of separately-named units

Dallas runs a Crimes Against Persons (CAPERS) Division that contains, as separate named units, Homicide / Special Investigations, Robbery, Assaults, and Special Victims. The Homicide/Special Investigations Unit page lists Lt. L. Porter as commander; three Homicide Squad supervisors (Sgts. Joseph Garza, Calvin Johnson, Cletus Judge) and a separate Special Investigations Unit sergeant (Sgt. Chuck Merritt). The Homicide Squads' scope is enumerated as Murder, Capital Murder, Manslaughter, Criminally Negligent Homicide, Suicide, Abuse of Corpse, and Unexplained/Natural Deaths. SIU is the officer-involved-shooting analog.

Detective headcount: not on the page. The literature-review memo cites the contraction from 28 (2017) to 16 (2018) under Chief Hall, and ~13 in May 2019 per NBC DFW's Bryan Riser coverage. By 2024, the unit has rebuilt under Chief García but the rebuilt number is not on the public page. PIA needed.

Confidence: HIGH on the scope coding; HIGH on the supervisor structure; LOW on annual headcount 2018-2025.

### Fort Worth — HOM-only Homicide Unit, separate from Major Case Unit (overrides the prompt assumption)

The prompt asked me to check whether FWPD's "Major Case Unit" is its homicide function. It is not. FWPD operates *both* a Homicide Unit (14 detectives per WFAA, 2024; work in pairs; rotate on-call weekends) and a Major Case Unit, both under Criminal Investigations (Capt. C. Harn). The Major Case Unit handles officer-involved shootings and other significant incidents, not routine homicides. FWPD also runs a separately-named Cold Case Unit. Self-reported clearance has been very high (93% 2023, 88% 2024) — the literature-review memo's note about a 2020 self-report/FBI clearance discrepancy (72% vs. 55%) still stands as a measurement caveat for that earlier year.

The 14-detective figure is 2024-vintage. The 2022-specific headcount is the open PIA question.

Confidence: HIGH on the scope coding; HIGH on the recent detective count but LOW for 2022.

### Austin — HOM-only Homicide Unit + dedicated Cold Case/Missing Persons Unit (the most-publicly-documented in the universe)

APD publishes the most detailed homicide unit structure of any TX city: 16 detectives + 2 sergeants in the Homicide Unit; 7 detectives + 1 sergeant in a separate Homicide Cold Case/Missing Persons Unit. Scope of Homicide Unit: "all homicides, accidental deaths (non-traffic related), suicides, and deaths of a suspicious or undetermined nature." Robbery is separate. This is the cleanest dedicated-squad model in the state.

Note: these figures are current (2024). The 2022 figures may have been different given the chaotic post-2020 budget-cut-and-restoration story documented in the identification-strategy memo. PIA needed for year-by-year 2019-2024 headcount. Worth pairing this with the published APD 2023 100% clearance announcement to test whether the headcount and clearance moved together.

Confidence: HIGH on current scope and staffing; MEDIUM on 2022-specific staffing.

### Corpus Christi — Robbery/Homicide combined unit (the canonical "Robbery/Homicide" model)

CCPD operates a Robbery/Homicide Unit per the public press releases ("Robbery/Homicide Detectives and Forensic Services" jointly dispatched to homicide scenes). This is the cleanest "Robbery/Homicide" combined-unit example in the universe — analogous to LAPD's RHD model. The Investigations Bureau page references an organizational chart PDF I could not retrieve; sub-unit staffing is not on the public page.

CCPD's 2022 number (41 per FBI, 41-44 per Caller-Times) was the highest in the published Corpus Christi annual record at the time per the local press.

Confidence: HIGH on the scope coding; LOW on staffing.

### Lubbock — Multi-agency Metropolitan Special Crimes Unit (the structural outlier)

Lubbock's homicide investigative function runs through the Metropolitan Special Crimes Unit, a multi-agency unit that pulls personnel from Lubbock PD, Lubbock County Sheriff, and other Lubbock-area agencies. This is fundamentally different from a single-agency squad: MSCU's case-assignment, supervisory chain, and detective FTE-by-agency-of-record are governed by an inter-agency memorandum of understanding I have not located publicly.

This makes Lubbock the structural outlier in the universe. For the project's purposes, it likely needs to be treated as either (a) its own category, requiring a separate PIA framework (to LPD *and* LCSO simultaneously), or (b) excluded from the per-city detective-FTE analysis on the grounds that the unit of analysis is wrong.

Note also the local-press-vs-FBI count gap (34 vs. 26). The press count likely includes manslaughters and possibly some non-criminal "homicide investigations" later determined non-criminal.

Confidence: HIGH that MSCU is the operational lead; LOW on everything else.

### Amarillo — HOM-only Homicide Unit since 2017 (post-task-force transition)

Amarillo presents a structurally interesting case: the unit was originally the "Special Crimes Unit," a Potter/Randall/APD multi-jurisdictional task force created in 1981 — analytically similar to Lubbock's current MSCU model. In 2017, APD reorganized it into a single-agency Homicide Unit (Lt. James Clements; Capt. Erick Bohannon over CID). That 2017 transition is itself a candidate natural-experiment, though sample size at one city makes formal identification impossible.

Detective headcount: not on public pages. PIA needed. The local-press-vs-FBI count gap (28 vs. 23) is consistent with the Lubbock pattern — local press likely counting manslaughters.

Confidence: MEDIUM on scope (it's the public page's framing but I want to confirm there hasn't been a quiet re-merger with another case type); LOW on staffing.

### El Paso — Crimes Against Persons unit (the strongest "omnibus" case in the universe)

EPPD's Crimes Against Persons unit (Lt. Alfred Lowe overseeing since 2004 — per the only public source I could find, which is a 2011 Police1.com article) handles "murders, unattended deaths, sexual assaults, kidnappings, home invasions and officer-involved shootings." That is the broadest case mix in the universe — every case type the other departments split off into specialized units (Sex Crimes, Robbery, OIS, etc.) is bundled into one unit at EPPD.

The 15-detective figure is 2011-vintage. By 2026 standards that number is almost certainly wrong (EPPD has expanded materially over the intervening 15 years), but no more recent source is on the public web. The literature review's note that EPPD has historically solved 102 of 106 homicides since 2004 (96%) reflects a department-reported figure with an exceptional track record — but per-detective workload calculations require knowing the actual current headcount and the *non-homicide* case load on the same detectives.

Confidence: MEDIUM on scope (the 2011 article is unambiguous, but I want a current verification); LOW on staffing — the 15-detective figure should not be relied on for any 2022 analysis.

### Killeen (borderline) — Robbery-Homicide combined unit under CID

Per KilleenPD news releases throughout 2022, the unit name is the "Criminal Investigation Division Robbery-Homicide Unit." Sgt. Neal Holtzclaw is one of the public-facing supervisors. CID is commanded by Commander Ronnie Supak; CID's broader scope spans "investigations of persons, property, juvenile, burglaries, warrants, narcotics and prostitution" but homicide and robbery are bundled in the named Robbery-Homicide Unit subdivision. This is structurally identical to the Corpus Christi model.

Killeen's 19-per-FBI / 22-per-press gap is the borderline-inclusion case for the universe.

Confidence: HIGH on scope coding; LOW on detective headcount.

---

## Cross-cutting observations

### How much organizational heterogeneity is there?

For a research project that wants to compare detective FTE against homicide caseload, the universe's organizational variation is substantively meaningful:

- **5 of 9 (or 5 of 10 with Killeen) are HOM-only dedicated squads**: Houston, Dallas, Fort Worth, Austin, Amarillo. These are the cities where "detective FTE / homicide" is closest to a clean ratio.
- **2 are combined HOM + aggravated-assault units**: San Antonio (explicitly named "Homicide & Assault"), El Paso (Crimes Against Persons, the broadest scope in the universe). Per-detective-per-homicide ratios for these cities are *inflated capacity estimates* relative to the dedicated-squad cities, because the same detectives are also working aggravated assaults, sex crimes (in EPPD), kidnappings, OIS.
- **2 are HOM + robbery combined units**: Corpus Christi, Killeen. Same logic — per-detective capacity is inflated relative to dedicated squads.
- **1 is a multi-agency task force**: Lubbock. The unit-of-analysis problem is severe; per-city detective FTE may not be defined.
- **0 are general-assignment.** Even the smallest cities in the universe specialize their homicide function.

### Modal structure

The modal structure is "HOM-only dedicated squad" (5 of 9). But the modal *case count* sits in the combined-scope cities: SAPD alone has 233 homicides on a combined HOM + assault unit, and EPPD's 22 are on a 6-case-type omnibus unit. So if we're weighting by cases-at-risk-of-misanalysis, the combined-scope cities dominate the universe.

### Outliers

- **Lubbock's MSCU**: the only multi-agency task force in the universe. Materially different unit of analysis from the others.
- **San Antonio's Homicide & Assault**: the only universe city whose homicide unit *explicitly names another case type in the unit's own name*. The closest direct evidence that the "homicide unit" framing is misleading without scope qualification.
- **El Paso's Crimes Against Persons**: the broadest scope (6 case types).
- **Amarillo's 2017 SCU-to-Homicide-Unit transition**: the only documented within-city organizational restructuring in the universe; structurally interesting but too small a city alone to support causal identification.
- **Houston's 2021 ~20-property-detective absorption**: the only documented within-city *expansion* shock in the universe; this is the project's primary natural-experiment candidate (per `docs/identification-strategy.md`).

### Implications for the "detectives per homicide" ratio

If we naively compute detectives-per-homicide using each city's *named-homicide-unit detective count* as the numerator and FBI homicide count as the denominator, the resulting ratio would:

1. **Over-state effective capacity in San Antonio, El Paso, Corpus Christi, and Killeen** by a factor that depends on the share of unit caseload that is non-homicide. In SAPD's case, aggravated assault charges alone in San Antonio likely run 4,000-5,000 per year — orders of magnitude higher than the homicide count. If the same detectives carry any non-trivial share of those cases, the "homicides per detective" denominator is dominated by non-homicide work.
2. **Compare incommensurable units in Lubbock**, where MSCU's homicide-detective FTE is a function of an inter-agency MOU rather than LPD's own staffing decision.
3. **Be roughly correct in Houston, Dallas, Fort Worth, Austin, and Amarillo** — the dedicated-squad cities — modulo the cold-case unit / SIU / gang-squad sub-allocations that affect on-call investigation capacity.

The implication for the research design is significant: any cross-city detective-FTE-to-clearance comparison needs to either (a) restrict to the HOM-only dedicated-squad cities (Houston, Dallas, Fort Worth, Austin, Amarillo, with N=5 that is uncomfortably small for cross-sectional inference); (b) collect and use a *scope-adjusted FTE* — only the share of detective time the agency reports as devoted to homicide — which requires PIA fields most departments will not have at hand; or (c) explicitly model unit scope as a covariate, with separate fixed effects or interaction terms for the combined-unit cities. Option (c) is the most data-flexible but requires being honest that you are estimating something different in SAPD/EPPD/CCPD than in HPD/DPD/FWPD/APD/Amarillo.

The naive ratio comparison — what most journalistic accounts and even some prior academic work has done — *overstates the analytic claim* of the staffing variable. The descriptive heterogeneity documented here is itself a finding worth foregrounding in any publication, independent of whether the substantive staffing-vs-clearance result turns out positive, null, or negative.

---

## What we still need PIA to get

Per-city gap summary:

- **Houston**: Annual headcount FY2019-FY2025 for Homicide Squads vs. Cold Case Squad vs. Gang Squad vs. SIU; specific squad assignments for the ~20 detectives transferred in March 2021; civilian analyst FTE attached to Homicide Division; Captain Zia tenure dates.
- **San Antonio**: Detective and sergeant headcount in Homicide & Assault; the share of unit caseload by case type (homicide vs. aggravated assault vs. suicide vs. overdose vs. other death); whether 2022 staffing was temporarily expanded for the 53-victim Quintana Road event; cold case detective count and whether it is a sub-unit of Homicide & Assault or separate.
- **Dallas**: Squad-by-squad detective count 2018-2025 spanning the Hall contraction and the García rebuild; civilian analyst FTE in CAPERS; reconciliation of the self-reported vs. FBI clearance discrepancy (would require asking DPD's own books how 2020 was coded relative to FBI submission).
- **Fort Worth**: 2022-specific detective headcount (the 14 figure is 2024); civilian analyst FTE; Major Case Unit scope and headcount (to confirm it does not absorb homicide cases under any circumstance); sergeant and supervisor count.
- **Austin**: 2022-specific Homicide Unit and Cold Case/Missing Persons Unit headcounts (the 16+2 / 7+1 figures are 2024-vintage); civilian analyst FTE attached to Homicide; lieutenant identification; whether the cold case unit existed at the same staffing in 2022.
- **Corpus Christi**: Detective and supervisor headcount in Robbery/Homicide; split of caseload between robbery and homicide; cold case capacity; civilian analyst FTE; bureau commander identification.
- **Lubbock**: Detective FTE by agency-of-record (LPD vs. LCSO vs. other) within MSCU; MSCU governance MOU; case-assignment protocol; cold case capacity within MSCU; whether LPD maintains *any* parallel internal homicide function.
- **Amarillo**: Annual detective headcount 2017-2025 spanning the SCU-to-Homicide-Unit transition; sergeant count; civilian analyst FTE; whether cold case capacity exists; whether any multi-agency liaison was retained post-2017.
- **El Paso**: Current (2022-2025) detective headcount (the 15-detective figure is 13 years old); current sergeant/lieutenant identification; civilian analyst FTE; whether any cold case specialization exists; share of unit caseload by case type — this is the highest-priority "current scope" PIA in the universe.
- **Killeen** (if included): Detective and supervisor headcount in CID Robbery-Homicide Unit; case-mix between robbery and homicide; cold case capacity; civilian analyst FTE.

The PIA template (per `docs/case-level-approach.md` §recommended-next-steps item 2) should explicitly ask for *all* of these — detective FTE by sub-unit, civilian analyst FTE, supervisor count, scope of cases handled, and a year-end snapshot for each year 2019-2024 — in the first wave, citing the basic-information framework under §552.108(c).

---

## What I could not verify and would flag

- **The 2022 Crime in Texas Annual Report PDF** at dps.texas.gov is binary-encoded and could not be parsed via WebFetch. The 47.94% statewide clearance figure cited in secondary sources should be confirmed against a manually-downloaded copy before any publication.
- **Houston's 2022 homicide count** has three published values circulating: 437 (FBI/CDE via city-data), 435 (HPD self-report widely cited in Click2Houston and ABC13 reporting), and 399 (one secondary aggregator). The 437 figure is the FBI submission and should be the headline.
- **El Paso's "15 detectives" figure** is from 2011 (Police1.com). It is the only specific EPPD Crimes Against Persons number on the public web. It must be re-verified before any 2022 analysis quotes it.
- **The SAPD General Manual Procedure 302** appears to formally enumerate SAPD's investigative units but the PDF I located is a scanned image and not extractable. A clean copy may be obtainable from the SAPD policy portal directly or via PIA.
- **The Lubbock MSCU governance structure** is referenced in news coverage but I could not locate the underlying MOU or any official MSCU organizational page. Whether MSCU has formal officer-of-record assignments per agency is unverified.
- **Killeen's 19-vs-22 count gap** could be a manslaughter inclusion issue or an FBI submission lag. Worth one targeted question to KPD records in the universe-cleanup phase.

---

## Bibliography (sources used for this memo)

**Universe / count sources (FBI/UCR):**

- FBI Crime Data Explorer. https://cde.ucr.cjis.gov/
- 2022 Crime in Texas Annual Report. https://www.dps.texas.gov/sites/default/files/documents/crimereports/22/2022cit.pdf (binary; not parsed)
- City-data.com per-city crime statistics pages (direct mirror of FBI Table 8): Houston, Dallas, San Antonio, Austin, Fort Worth, Corpus Christi, Lubbock, Amarillo, El Paso, Arlington, Pasadena, Beaumont, Killeen, Wichita Falls, Tyler

**City-specific homicide count cross-checks:**

- Houston: Click2Houston Dec 2022 "Houston turns corner in 2022 as city sees fewer homicides." https://www.click2houston.com/news/local/2022/12/31/houston-turns-corner-in-2022-as-city-sees-fewer-homicides/
- San Antonio: KSAT Oct 2023 "New FBI data shows SAPD violent crime reports hit all-time high in 2022." https://www.ksat.com/news/local/2023/10/19/new-fbi-data-shows-sapd-violent-crime-reports-hit-all-time-high-in-2022/
- Dallas: WFAA Jan 2023 "By the numbers: A look at Dallas' violent crime statistics from 2019 through 2022." https://www.wfaa.com/article/news/crime/dallas-crime-statistics-murder-assault-2019-2022/287-2c1ccb8b-f1aa-448e-86c0-276a5b25d0bb
- Fort Worth: Fort Worth Report (April 2024) fact brief on FW vs. SF 2022 homicide rate. https://fortworthreport.org/2024/04/30/fact-brief-did-fort-worth-have-a-higher-homicide-rate-than-san-francisco-in-2022/
- Austin: NICJR "Austin, Texas — GUN VIOLENCE PROBLEM ANALYSIS" (March 2024). https://nicjr.org/wp-content/uploads/2024/03/Austin-GVPA-3.2024.pdf
- Corpus Christi: Caller-Times reporting on 2022 record (cited by Yahoo News aggregator). https://www.yahoo.com/news/corpus-christi-had-many-homicides-090133906.html
- Lubbock: KTTZ March 2023 "Report shows slight increase in crime in 2022." https://radio.kttz.org/2023-03-30/report-shows-slight-increase-in-crime-in-2022-adding-to-already-high-lubbock-crime-rate
- Amarillo: thebullamarillo.com "Up Up Up: Record-Shattering Number of 28 Homicides for Amarillo in 2022." https://thebullamarillo.com/up-up-up-numbers-climb-for-amarillo-homicides-in-2022/
- El Paso: KTSM Jan 2024 "38 murders reported by EPPD in 2023." https://www.ktsm.com/local/el-paso-news/38-murders-reported-by-eppd-in-2023/
- Killeen: KDH (Killeen Daily Herald) Jan 2023 "Killeen had 22 homicides in 2022; half of them have been solved." https://kdhnews.com/news/local/killeen-had-22-homicides-in-2022-half-of-them-have-been-solved/article_882b474e-8948-11ed-a511-976eff6e6e41.html
- Wichita Falls: Texomas Home Page (Dec 2022) "Wichita Falls sees record homicide number in 2022." https://www.texomashomepage.com/news/local-news/wichita-falls-sees-record-homicide-number-in-2022/

**Unit organization sources:**

- Houston: HPD Homicide Division page. https://www.houstontx.gov/police/divisions/homicide/index.htm ; HPD Robbery Division page. https://www.houstontx.gov/police/robbery/ ; HPD Major Offenders Division page. https://www.houstontx.gov/police/divisions/major_offenders/index.htm ; ABC13 March 2021 "Houston PD officers being moved to homicide division." https://abc13.com/houston-crime-homicide-rate-police-department-understaffed/10422191/
- San Antonio: SAPD Homicide & Assault Division page. https://www.sa.gov/Directory/Departments/SAPD/About/Divisions/Homicide-Assault ; SAPD Divisions overview. https://www.sa.gov/Directory/Departments/SAPD/About/Divisions ; SAPD General Manual Procedure 302 — Organization. https://sacdla.com/wp-content/uploads/2020/03/302-Organization-12.pdf (PDF not extractable; flagged for PIA-and-manual-pull)
- Dallas: DPD Homicide/Special Investigations Unit. https://www.dallaspolice.net/division/crimeagainstpersons/homicideunit ; DPD Org Chart. https://www.dallaspolice.net/Shared%20Documents/DPDOrgChart.pdf (not extractable via WebFetch); DPD Beat blog homicide category. https://dpdbeat.com/category/homicide/
- Fort Worth: FWPD Cold Cases page. https://police.fortworthtexas.gov/Crime-Public-Info/Cold-Cases ; WFAA "Inside Fort Worth's Homicide Unit." https://www.wfaa.com/article/features/fort-worth-police-homicide-unit-detectives-obrien-and-cedillo-have-solved-most-shocking-complex-murder-cases/287-4bd55c7d-2562-4208-b539-740f90806f4a
- Austin: APD Homicide Unit page. https://www.austintexas.gov/police/divisions/homicide ; APD Cold Case Unit page. https://www.austintexas.gov/page/apd-cold-case-unit ; APD 2023 100% clearance press release. https://www.austintexas.gov/news/austin-police-department-homicide-unit-achieves-100-clearance-rate-2023-first-time-2005
- Corpus Christi: CCPD Investigations Bureau page. https://www.corpuschristitx.gov/department-directory/police-department/command-staff-and-bureaus/investigations-bureau/ ; CCPD Blotter. https://ccpdblotter.com/
- Lubbock: KCBD (Oct 2025) "Lubbock Metropolitan Special Crimes Unit asking for public's help." https://www.kcbd.com/2025/10/21/lubbock-metropolitan-special-crimes-unit-asking-publics-help-identifying-persons-interest-september-south-lubbock-homicide/ ; Lubbock PD department directory. https://ci.lubbock.tx.us/departments/police-department/about-us/department-directory
- Amarillo: APD Homicide Unit / Special Crime page. https://www.amarillopolice.org/special-crimes ; APD Criminal Investigations Division page. https://www.amarillopolice.org/detective ; APD 2023 Annual Report. https://www.amarillopolice.org/Resources/Amarillo%20Police%20Department%20Annual%20Report%20for%2020232023.pdf
- El Paso: Police1.com (2011) "El Paso's homicide clearance rate: 102 of 106 murders since '04." https://www.police1.com/investigations/articles/el-pasos-homicide-clearance-rate-102-of-106-murders-since-04-GIsNVmKKEayBiLKl/ ; EPPD page. https://www.elpasotexas.gov/police-department/
- Killeen: KilleenPD News. https://killeenpdnews.com/ ; Killeen city Police page. https://www.killeentexas.gov/231/Police ; Killeen Daily Herald. https://kdhnews.com/

**Related cross-cutting:**

- Jeff Asher, "Deep in the Heart of Texas Crime Data." https://jasher.substack.com/p/deep-in-the-heart-of-texas-crime
- BeautifyData Texas 2022 murder rate ranking. https://beautifydata.com/united-states-crimes/fbi-ucr/2022/ranking-of-cities-by-crime-rate-by-crime-type-per-state/murder-and-nonnegligent-manslaughter/texas

---

## Robbery and aggravated assault units in the HOM-only cities

Follow-up to the May 2026 memo. Object: the prior memo identified 5 universe cities (Houston, Dallas, Fort Worth, Austin, Amarillo) as running HOM-only dedicated homicide squads. For a within-city, across-crime-category clearance design, we also need to know whether those same departments run *separate, dedicated* units for robbery and for aggravated assault. If yes, the research design can compare how detective-per-case ratios map to clearance across three crime categories within the same department — a comparison that absorbs unobserved city-level factors (chief, DA, witness culture, gun availability). If no — if robbery and aggravated assault are bundled into general-assignment rotations or omnibus "Major Crimes" catchalls — the within-city comparison loses traction.

### TL;DR

- **Three of five HOM-only cities (Dallas, Austin, Houston) run cleanly separate robbery and aggravated assault units.** Dallas via separately-named CAPERS units (Homicide, Robbery, Assaults, Special Victims). Austin via three distinct units with publicly disclosed FTE: Homicide (16+2), Robbery (18 detectives + supervisors), Aggravated Assault (16 detectives). Houston via three separate divisions: Homicide Division, Robbery Division, and Major Assaults Division (the last specifically scoped to "non-family, adult assaults in which the complainant is expected to survive") plus a separate Family Violence Division for domestic-violence assaults.
- **Fort Worth is partial.** A dedicated Homicide Unit and a dedicated Robbery Unit both exist under Investigative & Support Command, plus a separate Gun Violence Investigations unit. But no public source names a distinct "Aggravated Assault Unit"; FWPD references Domestic Violence and Sexual Assault sub-units, suggesting non-DV aggravated assaults may be worked across multiple units rather than in a single dedicated bureau.
- **Amarillo is *not* HOM-only-style for robbery and AA — it bundles robbery + non-DV aggravated assault into a single Violent Crimes Unit.** Per APD's CID page and 2023 annual report context: the Violent Crimes Unit (Lt. T. Callahan) handles "robberies, discharging firearms, evading arrests, false ID, aggravated assaults and assaults with bodily injury that are not domestic violence related." 10 detective sergeants; 2,732 cases in 2023; ~280 cases per detective. Domestic Violence is a separate unit (same lieutenant). The HOM-only structure at Amarillo is the exception within APD's own CID, not the rule.
- **Nonfatal-shooting handling varies materially.** In Austin, nonfatal shootings explicitly route to the Aggravated Assault Unit (APD news releases consistently identify "Aggravated Assault Unit Detectives" as the investigators on shooting cases). In Fort Worth, a separately-named Gun Violence Investigations unit coordinates with Homicide and Robbery — closer to the Cook/Braga/Turchan/Barao "shooting-review-team" model. In Houston, the Major Assaults Division's own scope excludes nonfatal shootings and attempted murders, which suggests those route either to Homicide or to a gang/violent-offender unit (PIA needed to confirm). In Dallas, public sources do not specify; the Assaults Unit and Homicide Unit both appear to touch shooting cases. Amarillo bundles "discharging firearms" inside the Violent Crimes Unit.

### Houston

HPD runs three distinct divisions covering homicide, robbery, and aggravated assault. **Robbery Division** ("robbery offenses, theft from person and extortion") has four sub-units: Administrative, Investigative Squads (geographically distributed at police stations), Bank Squad (joint with FBI Bank Robbery Task Force), and Violent Offender Squad (serial/violent cases). Scope is all robbery types, including aggravated robbery and carjacking by implication, plus extortion and theft from person. **Major Assaults Division** is explicitly scoped to "non-family, adult assaults in which the complainant is expected to survive" — that is, stranger and public-place aggravated assaults excluding domestic violence and excluding fatal cases. Listed offense types: hate crimes, deadly conduct, harassment, road rage, terroristic threats, and non-in-progress kidnappings. A separate **Family Violence Division** (the prior memo treated Major Assaults and Family Violence as a combined "MAFV Division" per news references, but HPD's own divisions page lists them as separate) handles assaults where the victim is connected to the offender. Nonfatal shootings are not explicitly named in any of these divisions' scopes — likely routed to Homicide Division (attempted murders are routinely worked by homicide squads in large US departments) or to the Gang Squad, but this needs PIA confirmation. **No public detective headcount for any of these three divisions.** Within-city comparison feasibility: HIGH on structural separation; LOW on quantification until PIA.

### Dallas

DPD's Crimes Against Persons (CAPERS) Division contains, as separately-named units, **Homicide/Special Investigations Unit**, **Robbery Unit**, **Assaults Unit**, and **Special Victims Unit**. The Assaults Unit is commanded by Lt. Mario Garcia (per DPD Beat blog references); its scope is aggravated assaults including those with family-violence elements (the public-facing material doesn't separately wall off domestic-violence aggravated assaults to a different unit, though SVU handles the sex-crime adjacent cases). The Robbery Unit, per NBC DFW coverage, includes a "Robbery and Violent Crime task force" component supervised at the sergeant level (Sgt. Ross Selverino in 2019 reporting; current supervisor unconfirmed). No public detective headcount for either unit; the contraction-and-rebuild story documented for DPD Homicide (28→16→13 in 2017-2019) almost certainly has parallels in Robbery and Assaults but is not publicly documented. Within-city comparison feasibility: HIGH on structural separation; the public-facing org chart is the cleanest in the universe; LOW on staffing.

### Fort Worth

FWPD's Investigative & Support Command (Deputy Chief Chad Mahaffey) contains the Homicide Unit (14 detectives, 2024) and a Robbery Unit. WFAA and FWPD press releases routinely reference "Homicide, Robbery and Gun Violence Investigations" as three distinct detective groups that share information on weapon-involved cases — so robbery is structurally separate from homicide. The picture for aggravated assault is *muddier*. FWPD has a Domestic Violence Unit and a Sexual Assault Unit, but no public source identifies a dedicated "Aggravated Assault Unit" or "Assault Unit" parallel to Dallas's. Non-DV, non-sexual aggravated assaults may be worked by patrol detectives, by Gun Violence Investigations (where firearms are involved), or by Major Case Unit (where significant). The 2023 Violent Crime Reduction Plan referenced "decreasing homicides, aggravated assaults and robberies" but did not name a dedicated aggravated assault investigative unit. Within-city comparison feasibility: PARTIAL — robbery is cleanly separate, aggravated assault is not cleanly bundled or unbundled.

### Austin

APD is the universe's most-publicly-documented department on this question, by a wide margin. Three separate units with disclosed FTE: **Homicide Unit** (16 detectives, 2 sergeants); **Robbery Unit** (18 detectives, 1 lieutenant, 2 sergeants, 1 crime analyst, 1 victim services counselor, 1 administrative assistant — scope: "robberies of individuals, businesses, and banks within the City of Austin"); **Aggravated Assault Unit** (16 detectives, per the 2022 Special Victims Intervention Unit presentation to the Commission for Women; 2022 caseload 2,392 cases). A separate **Domestic Violence Unit** (16 detectives, 2 sergeants, 8,007 cases in 2022) handles family-violence assaults; a small **Special Victims Intervention Unit** (1 sergeant + 1 detective + 4 officers) handles high-risk-of-escalation cases. Nonfatal shootings explicitly route to the Aggravated Assault Unit — APD news releases name "Aggravated Assault Unit Detectives" as the investigators on shooting cases. The 2023 Homicide 100%-clearance press release noted the Aggravated Assault Unit led investigations on four 2023 homicide cases and that the Violent Crimes Task Force (typically robberies) assisted on homicides — implying real cross-unit fluidity. Within-city comparison feasibility: HIGH on structural separation, HIGH on quantification, with current FTE publicly disclosed and 2022 caseloads documented.

### Amarillo

The structurally interesting finding: Amarillo is the only HOM-only city in the universe whose *robbery* and *aggravated assault* functions are *combined* into a single unit, not separated. APD's CID page lists six units: Homicide, Special Victims (sex crimes + children), **Violent Crimes (Lt. T. Callahan; "robberies and assaults")**, Domestic Violence (Lt. T. Callahan; "assaults and other crimes involving domestic partners"), Property Crimes, and General Investigations. Amarillo Tribune and APD's own 2023 reporting indicate the Violent Crimes Unit covered 2,732 cases in 2023 with 10 detective sergeants — robbery + non-DV aggravated assault + discharging firearms + related — averaging ~280 cases per detective. Two important implications: first, robbery and non-DV aggravated assault cannot be cleanly disentangled at Amarillo for any within-city comparison; second, the per-detective caseload (~280) in Violent Crimes is so much higher than what any Texas homicide-only squad would carry that any apples-to-apples comparison of "detective workload" across the three categories at Amarillo would mostly be picking up "homicide is much-better-resourced than robbery or assault per case" rather than anything about clearance technology. Within-city comparison feasibility: NO. Robbery and AA share one bureau, one supervisor, one detective pool.

### Cross-cutting observation

Five HOM-only cities, five different stories on the robbery + AA side. The HOM-only structure is *not* a predictor of separately-organized robbery and AA units. Three of five departments (Houston, Dallas, Austin) carry the dedicated-squad logic across all three violent-crime categories. One (Fort Worth) carries it for robbery but not cleanly for aggravated assault. One (Amarillo) abandons it entirely for robbery + AA, bundling them into a single Violent Crimes Unit. The takeaway is that organizational specialization at the homicide level does not generalize. A city can run a HOM-only squad as a prestige unit while running everything else through omnibus structures — which is exactly what Amarillo appears to do.

The Austin data also surfaces a substantive point worth carrying into the design: APD's *highest-caseload* unit by far (Domestic Violence, 8,007 cases on 16 detectives, ~500 cases per detective per year) is not the homicide unit; the homicide unit's per-detective caseload (65 homicides ÷ 16 detectives = ~4 cases/year) is two orders of magnitude lower. If "homicides per detective" is meant to proxy for "investigation capacity per case," it does not generalize as a measurement framework — DV detectives at APD operate at 100x the case density of homicide detectives in the same department. Any cross-category model has to take this capacity gradient seriously.

### Implications for the within-city three-category research design

Of the 5 HOM-only cities, **three (Austin, Dallas, Houston) support a clean three-category within-city design** in structural terms. Austin is the only one with fully-disclosed FTE on all three units; Dallas and Houston need PIA to quantify, but the structural separation is clear from the org chart. **Fort Worth is a borderline case** that would have to be either coded as two-category (homicide + robbery, with AA carried at the patrol level or distributed) or dropped from the three-category analysis. **Amarillo cannot support the three-category design** at all — robbery and AA share a unit.

That leaves N=3 (or N=4 with Fort Worth as two-category) as the within-city sample for a three-category clearance design. This is too small to be a *primary* identification strategy on its own. It is workable as a *robustness check* layered on top of cross-city designs: showing that the cross-city relationship between detective FTE and clearance holds within Austin, Dallas, and Houston when you compare homicide-detective-FTE-per-homicide to robbery-detective-FTE-per-robbery to AA-detective-FTE-per-AA, and survives the within-city fixed-effect absorption, would be a meaningful auxiliary test. But it is not a stand-alone strategy.

The deeper finding is that the within-city design *cannot* be applied uniformly across the universe even after restricting to the HOM-only cities. Heterogeneity in unit structure persists even within the "structurally simple" cohort, which is itself a finding worth noting in any methodology section.

### Sources used for this section

**City unit pages:**
- HPD Robbery Division. https://www.houstontx.gov/police/robbery/
- HPD Major Assaults Division. https://www.houstontx.gov/police/divisions/major_assaults/index.htm
- HPD Family Violence Division. https://www.houstontx.gov/police/divisions/family_violence/index.htm
- HPD Divisions overview. https://www.houstontx.gov/police/divisions/
- DPD Assaults Unit. https://www.dallaspolice.net/division/crimeagainstpersons/assaultsunit
- DPD Robbery Unit. https://www.dallaspolice.net/division/crimeagainstpersons/robberyunit
- FWPD Investigative & Support Command. https://police.fortworthtexas.gov/About/investigative-and-support-command
- FWPD Organizational Chart. https://police.fortworthtexas.gov/About-FWPD-Landing/Organizational-Chart
- APD Robbery Unit. https://www.austintexas.gov/police/divisions/robbery
- APD Domestic Violence Unit. https://www.austintexas.gov/department/family-violence-protection
- Amarillo PD CID. https://www.amarillopolice.org/detective
- Amarillo PD Special Crimes (Homicide Unit). https://www.amarillopolice.org/special-crimes

**News and audit:**
- WFAA "Fort Worth Police 2023 violent crime plan." https://www.wfaa.com/article/news/local/fort-worth-police-2023-violent-crime-plan/287-3cc0ecf9-1e7d-4ee3-acc8-95e963516553
- NBC DFW "Inside the Dallas Police Department's Robbery Unit." https://www.nbcdfw.com/news/local/inside-the-dallas-police-departments-robbery-unit/200066/
- Austin Commission for Women, APD Special Victims Intervention Unit presentation (DV/AA/Robbery FTE & caseload comparisons). https://bandc.crccheck.com/commission-women/431845-item-2-austin-police-department-special-victims-intervention-unit-presentation/
- APD 2023 100% clearance press release. https://www.austintexas.gov/news/austin-police-department-homicide-unit-achieves-100-clearance-rate-2023
- Amarillo Tribune "In-depth look at crime in Amarillo" (June 2024). https://amarillotribune.org/2024/06/14/an-in-depth-look-at-crime-in-amarillo/

**FBI/UCR 2022 crime counts (via city-data.com mirrors of FBI Table 8):**
- Houston: https://www.city-data.com/crime/crime-Houston-Texas.html (2022: 6,974 robberies; 17,663 aggravated assaults)
- Dallas: https://www.city-data.com/crime/crime-Dallas-Texas.html (2022: 2,175 robberies; 7,320 aggravated assaults) — note WFAA secondary reporting cites 2,227 and 5,816 respectively; the city-data Table-8 figures are the FBI submission.
- Fort Worth: https://www.city-data.com/crime/crime-Fort-Worth-Texas.html (2022: 689 robberies; 3,396 aggravated assaults)
- Austin: https://www.city-data.com/crime/crime-Austin-Texas.html (2022: 936 robberies; 3,689 aggravated assaults)
- Amarillo: https://www.city-data.com/crime/crime-Amarillo-Texas.html (2022: 203 robberies; 1,126 aggravated assaults)
- FBI Crime Data Explorer landing: https://cde.ucr.cjis.gov/

**PIA gaps (additions to the prior memo's PIA roster):**
- Houston: how nonfatal shootings and attempted murders are routed (Homicide vs. Gang Squad vs. Major Assaults); current Robbery Division detective headcount; current Major Assaults Division detective headcount.
- Dallas: Robbery Unit detective headcount; Assaults Unit detective headcount; whether the Assaults Unit handles all aggravated assaults including DV cases or whether DV is bundled at the patrol level.
- Fort Worth: whether an Aggravated Assault Unit exists separately from Gun Violence Investigations and Major Case Unit, and at what staffing.
- Austin: 2022-specific FTE (the 16/18/16 figures are from a 2022-vintage presentation but should be cross-checked against an APD-internal year-end snapshot); civilian analyst FTE across the three units.
- Amarillo: Violent Crimes Unit detective FTE in 2022 (the 10-detective-sergeant figure is 2023); whether discharging-firearms cases are formally distinct from aggravated assault inside Violent Crimes.
