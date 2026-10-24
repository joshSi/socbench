## 2024-05-18 - Replacing iterative row hashing with native polars write_ndjson
**Learning:** Writing jsonl files row by row in Python using `iter_rows` and `canonical_json` is extremely slow for large datasets in polars.
**Action:** Use polars `write_ndjson` combined with sorting columns `df.select(sorted(df.columns)).write_ndjson()` to emit sorted-key JSON objects deterministically and at native speed without breaking hashing constraints.
## 2024-10-24 - Push type casting to Polars Engine
**Learning:** Performing type casts using Python list comprehensions on Polars results inside Python loops is significantly slower than doing it within the Polars `.agg()` phase using `.cast()`. Polars' C/Rust vectorized backend optimizes casting better than standard Python loops.
**Action:** Always cast Polars columns using `.cast()` natively before calling `.to_list()` and iterating over results in Python.
