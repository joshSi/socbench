## 2024-05-18 - Replacing iterative row hashing with native polars write_ndjson
**Learning:** Writing jsonl files row by row in Python using `iter_rows` and `canonical_json` is extremely slow for large datasets in polars.
**Action:** Use polars `write_ndjson` combined with sorting columns `df.select(sorted(df.columns)).write_ndjson()` to emit sorted-key JSON objects deterministically and at native speed without breaking hashing constraints.

## 2025-02-15 - Optimizing Polars Python iteration with zip() and to_list()
**Learning:** Iterating over Polars DataFrames in Python using `iter_rows()` is remarkably slow because it materializes a dictionary for every row.
**Action:** Use `zip()` across multiple column `.to_list()` calls to achieve significantly faster iteration without the overhead of dictionary creation.
