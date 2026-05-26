# CLAUDE.md

This file provides guidance to Claude Code when working with code in this repository.

## Project

Empirical test of the thesis: **controlling for case-mix and city characteristics, cities with better homicide detective FTE ratios (detectives per homicide case) clear more homicides.** Author: Brennan Griffin (Texas Appleseed). Primary setting: Texas cities, sourced via Public Information Act requests; possible national comparison set for power and robustness.

The literature review (`docs/literature-review.md`) flags one consequential threat: **Bjerk 2022 (JELS)** finds a null on aggregate police budget → clearance in 50 large cities, robust to IV. The thesis only survives if "detective FTEs" is materially different from "aggregate police budget" — i.e., the *allocation* of staffing to homicide units is what matters, not the size of the wallet. The defensible framing is closer to Braga & Dusseault's 2018 Boston study: organizational bundles (initial-scene staffing thresholds, time-to-assignment discipline, civilian analyst capacity) that happen to require headcount, not headcount per se.

## Current state

- `docs/literature-review.md` — ~3,800 word synthesis of detective-staffing-and-clearance literature
- No data acquired yet
- No analysis code yet
- No PIA requests sent

## Commands

- `uv sync` — install / update dependencies (uv manages `.venv/`)
- `uv sync --group analysis` — add statsmodels, linearmodels, jupyter for analysis work
- `uv run pytest` — run tests

## Cross-cutting rules

- **Cite real papers only.** Every citation in `docs/` must be verifiable. Flag uncertain cites rather than papering over them.
- **Distinguish clearance-by-arrest from clearance-by-exception.** They are not interchangeable. Exception-rate inflation is a documented data-quality problem (Murder Accountability Project critique); the analysis must report both separately.
- **Pre-register before pulling outcome data.** Once a design is agreed, write it down in `docs/` before looking at clearance numbers. Protects against specification searching given small-N Texas panel.
- **Reproducibility.** Every data pull is scripted; API responses cached (`data/cache/`) so re-runs don't re-hit FBI CDE, Census, or city portals.
- **PIAs are public infrastructure.** Be polite, narrow, and patient. Don't fire vague omnibus requests at every TX city at once.

## Open scoping decisions (to settle with Brennan before writing analysis code)

1. **Sample**: Texas-only (10-20 cities with enough homicides for power) vs. Texas + national comparison set (50-100 cities). National helps power and gives off-the-shelf staffing data via LEMAS, but loses the PIA-driven detective-bureau granularity that is the project's actual contribution.
2. **Primary identification strategy**: Cross-city OLS with case-mix controls (weakest, but baseline); Houston synthetic control on the 2020→2022 clearance recovery; COPS hiring-grant IV. Pick one primary, one robustness.
3. **PIA priority list**: Houston, Dallas, San Antonio, Austin, Fort Worth are obvious. The 6-15 mid-size cities (Arlington, El Paso, Corpus, Plano, Lubbock, Laredo, Garland, Irving, Amarillo, McAllen, Killeen, Waco) are where most of the variance — and most of the PIA effort — lives.
4. **Outcome definition**: UCR clearance vs. FBI CDE NIBRS clearance vs. PIA-reported department clearance. They diverge (Dallas reported 78% to its own city council vs. 39% to FBI for 2020). Decide which is the headline and which is the audit.
