## 2024-05-18 - Replacing iterative row hashing with native polars write_ndjson
**Learning:** Writing jsonl files row by row in Python using `iter_rows` and `canonical_json` is extremely slow for large datasets in polars.
**Action:** Use polars `write_ndjson` combined with sorting columns `df.select(sorted(df.columns)).write_ndjson()` to emit sorted-key JSON objects deterministically and at native speed without breaking hashing constraints.
## 2026-10-05 - [Optimize Polars Row Iteration]
**Learning:** [Iterating over rows in polars using `iter_rows` in Python is slow for large datasets due to dictionary materialization.]
**Action:** [Use `zip` across individual column `.to_list()` outputs instead of `iter_rows` to avoid dictionary materialization overhead.]
