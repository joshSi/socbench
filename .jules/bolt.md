## 2024-05-18 - Replacing iterative row hashing with native polars write_ndjson
**Learning:** Writing jsonl files row by row in Python using `iter_rows` and `canonical_json` is extremely slow for large datasets in polars.
**Action:** Use polars `write_ndjson` combined with sorting columns `df.select(sorted(df.columns)).write_ndjson()` to emit sorted-key JSON objects deterministically and at native speed without breaking hashing constraints.

## 2024-10-29 - Polars `.to_list()` Native Typing
**Learning:** In Polars, calling `.to_list()` natively produces fully-typed nested Python lists (e.g. `[int, int]` instead of a generic untyped list needing conversion).
**Action:** When iterating through columns cast from Polars `to_list()`, avoid redundant Python list comprehensions like `[int(x) for x in row]` and directly assign them.

## 2024-11-11 - O(1) min/max indexing on sorted time series
**Learning:** For optimal performance when calculating min/max on monotonically sorted list slices derived from Polars (e.g., time series chunks), avoid O(N) `min()`/`max()` scans.
**Action:** Use O(1) direct index access instead (e.g., `tss[a]` and `tss[b-1]`).
