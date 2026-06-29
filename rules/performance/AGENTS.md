# Performance Rules

This directory defines render, bundle, list, and native bridge performance rules.

## Rendering

- Use memoization when there is measurable re-render cost.
- Split large calculations out of the render path, and use memoized selectors when needed.
- Optimize inline objects/functions only when there is an actual problem.
- Do not keep derived state in memory when it can be computed cheaply from owned source state.
- Avoid retaining large props, raw payloads, or closures longer than the component lifecycle requires.
- Hot render, parser, input, native bridge, and IO loops must not allocate fresh buffers or large arrays per frame/event/read when stable reusable storage is practical.
- Diagnostic fallbacks that force full redraws, full recomputation, or broad invalidation must be opt-in, named, and easy to disable after the original bug is covered by regression tests.

## Lists and Data

- Use virtualization for large lists.
- Constantize pagination, page size, and prefetch threshold values.
- Load images and assets at the required size.
- Large in-memory datasets need pagination, windowing, indexing, or eviction strategy.
- Cache entries must have clear keys, invalidation rules, and memory bounds or TTL.
- Front-trimming large collections with repeated whole-array copies is forbidden in hot paths; use bounded stores, ring buffers, logical start indexes, or batched compaction.

## Bridge and IO

- Limit native bridge call frequency and payload size.
- Constantize polling interval, debounce, and throttle values.
- Leave before/after measurements or reproducible evidence for performance improvements.
- Do not send raw large objects over native bridges or worker boundaries when a compact DTO is enough.
- Performance optimizations must preserve layer boundaries; do not bypass services/repositories just to save a small amount of code.
