## 2024-05-18 - Replacing iterative row hashing with native polars write_ndjson
**Learning:** Writing jsonl files row by row in Python using `iter_rows` and `canonical_json` is extremely slow for large datasets in polars.
**Action:** Use polars `write_ndjson` combined with sorting columns `df.select(sorted(df.columns)).write_ndjson()` to emit sorted-key JSON objects deterministically and at native speed without breaking hashing constraints.

## 2025-05-15 - Polars Series Iteration Overhead in List Comprehensions
**Learning:** When using `zip()` on Polars Series inside a list comprehension, it creates a lot of overhead. Converting the Series to Python lists using `.to_list()` first and zipping those is significantly faster (around ~20% faster depending on data size).
**Action:** When zipping polars columns, add `.to_list()` to avoid boundary crossing overhead.
