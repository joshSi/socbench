## 2024-05-18 - Replacing iterative row hashing with native polars write_ndjson
**Learning:** Writing jsonl files row by row in Python using `iter_rows` and `canonical_json` is extremely slow for large datasets in polars.
**Action:** Use polars `write_ndjson` combined with sorting columns `df.select(sorted(df.columns)).write_ndjson()` to emit sorted-key JSON objects deterministically and at native speed without breaking hashing constraints.
## 2024-10-21 - [Polars Python Loop Optimization]
**Learning:** For optimal Polars performance in Python loops within this codebase, direct Series iteration introduces significant dictionary materialization and Rust-to-Python boundary crossing overhead.
**Action:** Use `zip()` across individual column `.to_list()` outputs to avoid this overhead.
