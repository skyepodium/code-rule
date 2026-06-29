# Concurrency and Async Rules

This directory defines rules for asynchronous work, cancellation, and race conditions.

## Cancellation

- Fetches, subscriptions, timers, and background tasks must have cancellation or cleanup paths.
- Prevent state updates after component unmount.
- Use `AbortController` or the project's standard cancellation API.
- The layer that starts async work owns its cancellation unless ownership is explicitly transferred.
- Services that expose long-running work must expose cancellation, dispose, or reset behavior.
- Do not leave promises, subscriptions, observers, native listeners, or background tasks without a lifecycle owner.

## Race Conditions

- Screens that should reflect only the latest request must use request IDs, aborts, or stale guards.
- Consider simultaneous submits, duplicate taps, and fast route transitions.
- Optimistic updates must have failure rollback and conflict criteria.

## Timers and Schedulers

- Clean up intervals, timeouts, and animation frames.
- Constantize time values.
- Define pause and resume criteria for background/foreground transitions.
- Avoid unbounded queues. Define max size, drop policy, retry policy, or backpressure behavior for queued async work.
- For polling, define start, stop, visibility/background behavior, and duplicate-start prevention.
