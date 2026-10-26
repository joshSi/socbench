## 2024-05-18 - Replacing iterative row hashing with native polars write_ndjson
**Learning:** Writing jsonl files row by row in Python using `iter_rows` and `canonical_json` is extremely slow for large datasets in polars.
**Action:** Use polars `write_ndjson` combined with sorting columns `df.select(sorted(df.columns)).write_ndjson()` to emit sorted-key JSON objects deterministically and at native speed without breaking hashing constraints.
## 2025-02-12 - Redundant List Comprehensions on Polars Output
**Learning:** Calling `.to_list()` on an aggregated Polars column of lists natively produces fully-typed nested Python lists (e.g. `list[int]`). Repeating the type coercion via list comprehensions like `[int(x) for x in row]` incurs massive, unnecessary O(N) overhead per group when iterating rows sequentially.
**Action:** Always trust the types returned by `.to_list()` when correctly coerced inside Polars, and avoid redundant Python list comprehensions.
