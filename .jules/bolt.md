## 2024-05-18 - Replacing iterative row hashing with native polars write_ndjson
**Learning:** Writing jsonl files row by row in Python using `iter_rows` and `canonical_json` is extremely slow for large datasets in polars.
**Action:** Use polars `write_ndjson` combined with sorting columns `df.select(sorted(df.columns)).write_ndjson()` to emit sorted-key JSON objects deterministically and at native speed without breaking hashing constraints.
## 2025-02-12 - Lazily loading large JSON run artifacts
**Learning:** Loading large JSON artifacts (like `summary.json`) for every run in a directory during discovery is a major performance bottleneck when only a few runs match the desired filters.
**Action:** Parse only the lightweight `run_metadata.json` to filter runs by `dataset_hash` and `sample_seed` first, and defer parsing `summary.json` until the run is confirmed as a match.
