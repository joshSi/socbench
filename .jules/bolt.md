## 2024-05-18 - Replacing iterative row hashing with native polars write_ndjson
**Learning:** Writing jsonl files row by row in Python using `iter_rows` and `canonical_json` is extremely slow for large datasets in polars.
**Action:** Use polars `write_ndjson` combined with sorting columns `df.select(sorted(df.columns)).write_ndjson()` to emit sorted-key JSON objects deterministically and at native speed without breaking hashing constraints.
## 2024-05-18 - Replacing redundant list(set()) conversions for Polars .is_in() filters
**Learning:** Polars `.is_in()` works best when passed a Series or a list directly. Converting a unique Polars list output into a set and back into a list inside a filter introduces unnecessary Python object overhead without changing semantics.
**Action:** Preserve native list representations returned by Polars (like `.to_list()`) and pass them directly to `.is_in()`, avoiding redundant `list(set())` conversions for already distinct data.
