# data/

All subdirectories below are gitignored. This README is the only tracked file.

- `raw/` — original pulls from FBI CDE, NIBRS, Census ACS, and PIA response files. Never edit by hand; regenerate via `scripts/`.
- `processed/` — cleaned panel datasets ready for analysis. Built deterministically from `raw/`.
- `cache/` — HTTP response cache (SQLite). Lets re-runs replay without re-hitting external APIs.
- `tmp/` — scratch space; safe to delete.

If you add a new raw source, document its provenance (URL, pull date, license/terms) in `docs/data-sources.md`.
