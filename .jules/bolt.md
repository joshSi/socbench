## 2024-05-18 - Replacing iterative row hashing with native polars write_ndjson
**Learning:** Writing jsonl files row by row in Python using `iter_rows` and `canonical_json` is extremely slow for large datasets in polars.
**Action:** Use polars `write_ndjson` combined with sorting columns `df.select(sorted(df.columns)).write_ndjson()` to emit sorted-key JSON objects deterministically and at native speed without breaking hashing constraints.
## 2025-02-23 - [Polars: Redundant Comprehensions Overhead]
**Learning:** `.to_list()` natively produces fully-typed nested Python lists in Polars. Applying redundant Python list comprehensions (e.g. `[int(x) for x in row]`) on its output introduces unnecessary iteration and type casting, causing significant performance overhead during loops.
**Action:** Avoid Python list comprehensions on `.to_list()` outputs. Instead, cast columns directly via `.cast()` in Polars before converting to lists, and assign directly.
