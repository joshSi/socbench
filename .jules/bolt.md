## 2024-05-18 - Replacing iterative row hashing with native polars write_ndjson
**Learning:** Writing jsonl files row by row in Python using `iter_rows` and `canonical_json` is extremely slow for large datasets in polars.
**Action:** Use polars `write_ndjson` combined with sorting columns `df.select(sorted(df.columns)).write_ndjson()` to emit sorted-key JSON objects deterministically and at native speed without breaking hashing constraints.

## 2025-02-12 - Remove redundant list comprehensions on Polars .to_list() outputs
**Learning:** Polars `.to_list()` natively produces fully-typed nested Python lists (e.g., list of integers). Performing a Python list comprehension (like `[int(x) for x in row]`) on its output is completely redundant and adds significant overhead in tight loops.
**Action:** Apply all necessary type casting natively in Polars (using `.cast()`) inside the `.agg()` prior to list conversion, and assign the output of `.to_list()` elements directly without looping over them again in Python.
