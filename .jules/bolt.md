## 2024-05-18 - Replacing iterative row hashing with native polars write_ndjson
**Learning:** Writing jsonl files row by row in Python using `iter_rows` and `canonical_json` is extremely slow for large datasets in polars.
**Action:** Use polars `write_ndjson` combined with sorting columns `df.select(sorted(df.columns)).write_ndjson()` to emit sorted-key JSON objects deterministically and at native speed without breaking hashing constraints.

## 2025-02-12 - Replacing Python list comprehensions with Polars native type casting inside `.agg()`
**Learning:** Performing list comprehension conversions (e.g. `[int(x) for x in row_flow_ids]`) inside Python loops evaluating Polars rows adds massive overhead. Even though `iter_rows()` is avoided by zipping `.to_list()` columns, the items within those list columns still required O(N) iteration in Python.
**Action:** Always push type casting directly into the native Polars engine using `.cast()` inside the `.agg()` expression (e.g. `pl.col("_flow_id").cast(pl.Int64)`) prior to list conversion, which avoids the need for Python-side element-wise iteration entirely.
