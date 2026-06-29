# Performance Rules

This directory defines render, bundle, list, and native bridge performance rules.

## Rendering

- Use memoization when there is measurable re-render cost.
- Split large calculations out of the render path, and use memoized selectors when needed.
- Optimize inline objects/functions only when there is an actual problem.

## Lists and Data

- Use virtualization for large lists.
- Constantize pagination, page size, and prefetch threshold values.
- Load images and assets at the required size.

## Bridge and IO

- Limit native bridge call frequency and payload size.
- Constantize polling interval, debounce, and throttle values.
- Leave before/after measurements or reproducible evidence for performance improvements.
