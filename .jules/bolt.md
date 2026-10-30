## 2024-05-18 - Replacing iterative row hashing with native polars write_ndjson
**Learning:** Writing jsonl files row by row in Python using `iter_rows` and `canonical_json` is extremely slow for large datasets in polars.
**Action:** Use polars `write_ndjson` combined with sorting columns `df.select(sorted(df.columns)).write_ndjson()` to emit sorted-key JSON objects deterministically and at native speed without breaking hashing constraints.

## 2024-10-29 - Polars `.to_list()` Native Typing
**Learning:** In Polars, calling `.to_list()` natively produces fully-typed nested Python lists (e.g. `[int, int]` instead of a generic untyped list needing conversion).
**Action:** When iterating through columns cast from Polars `to_list()`, avoid redundant Python list comprehensions like `[int(x) for x in row]` and directly assign them.

## 2024-05-18 - Polars Native Typing
**Learning:** Polars `.to_list()` outputs fully-typed nested Python lists, removing the need for redundant Python list comprehensions and explicit casting.
**Action:** Avoid explicit python types casting on output of `.to_list()`.
