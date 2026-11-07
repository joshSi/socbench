1. **Optimize `ts_start_min` and `ts_start_max` in `assign_eval_units`**:
    - `src/socbench/index.py` sorts records by `ts_start` (`sort(["src_ip", "dst_ip", "ts_start", "_flow_id"])` and `sort(["src_ip", "bucket", "ts_start", "_flow_id"])`).
    - The aggregated lists of `tss` (timestamps) are therefore monotonically increasing within each group.
    - Inside the chunking loops:
        - `ts_start_min=min(tss[a:b])` can be optimized to `ts_start_min=tss[a]`
        - `ts_start_max=max(tss[a:b])` can be optimized to `ts_start_max=tss[b-1]`
    - This changes O(N) operations within the loop to O(1) array accesses. We avoid the overhead of slicing the list and scanning it with `min()` and `max()`.

2. **Pre-commit Checks**: Run `pnpm lint`/`pnpm test` equivalents via `uv`. Update `.jules/bolt.md` with critical learning.
