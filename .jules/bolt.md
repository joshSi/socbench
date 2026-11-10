## 2024-05-18 - Replacing iterative row hashing with native polars write_ndjson
**Learning:** Writing jsonl files row by row in Python using `iter_rows` and `canonical_json` is extremely slow for large datasets in polars.
**Action:** Use polars `write_ndjson` combined with sorting columns `df.select(sorted(df.columns)).write_ndjson()` to emit sorted-key JSON objects deterministically and at native speed without breaking hashing constraints.

## 2024-10-29 - Polars `.to_list()` Native Typing
**Learning:** In Polars, calling `.to_list()` natively produces fully-typed nested Python lists (e.g. `[int, int]` instead of a generic untyped list needing conversion).
**Action:** When iterating through columns cast from Polars `to_list()`, avoid redundant Python list comprehensions like `[int(x) for x in row]` and directly assign them.

## 2026-11-10 - O(1) Index Access for Min/Max on Monotonically Sorted Polars Chunks
**Learning:** Polars list chunks produced from data grouped and sorted by timestamp are inherently monotonically sorted. Using Python's `min()` and `max()` on slice lists (e.g. `min(tss[a:b])`) introduces O(N) complexity for something that is already sorted.
**Action:** When calculating minimum and maximum values on list slices that are monotonically sorted from Polars, use O(1) direct index access (e.g. `tss[a]` and `tss[b-1]`) to bypass unnecessary scanning overhead.
