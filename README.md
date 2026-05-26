# Homicide clearance rates and budgets

Empirical research project testing whether, controlling for case-mix and city characteristics, U.S. cities with better homicide detective FTE ratios clear more homicides. Primary setting: Texas cities, with possible national comparison set for robustness.

Author: Brennan Griffin.

## Status

Scoping phase. Literature review complete (`docs/literature-review.md`). No data acquired or analysis written yet.

## Layout

- `src/` — analysis code
- `data/` — raw API pulls, PIA responses, processed panels (all gitignored except `data/README.md` describing layout)
- `docs/` — literature review, research design, methodology memos
- `scripts/` — one-off data pulls, PIA submission helpers
- `notebooks/` — exploratory analysis
- `configs/` — per-city / per-source YAML
- `tests/` — analysis correctness tests

## Setup

```
uv sync
uv sync --group analysis   # pulls statsmodels, linearmodels, jupyter, etc.
```
