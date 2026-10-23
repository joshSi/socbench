## 2024-05-18 - Replacing iterative row hashing with native polars write_ndjson
**Learning:** Writing jsonl files row by row in Python using `iter_rows` and `canonical_json` is extremely slow for large datasets in polars.
**Action:** Use polars `write_ndjson` combined with sorting columns `df.select(sorted(df.columns)).write_ndjson()` to emit sorted-key JSON objects deterministically and at native speed without breaking hashing constraints.
## 2024-10-23 - Polars Cast vs Python List Comprehension
**Learning:** For optimal Polars performance in Python loops, casting columns to exact types via `.cast()` during `.agg()` is much faster (roughly 2x) than extracting to a generic list and converting items using a python list comprehension inside the loop.
**Action:** Always prefer Polars native `.cast()` operations in the aggregation/transformation phase rather than manipulating lists in python space, especially within performance-critical inner loops where overhead is magnified.
