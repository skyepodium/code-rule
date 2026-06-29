# Testing Rules

This directory defines unit, integration, and component test rules.

## Basic Principles

- Add tests first or update existing tests for changed behavior.
- For bug fixes, lock the symptom with a failing regression test before fixing it.
- Test names must describe expected behavior. Do not use meaningless names like `works` or `test1`.
- Tests verify public interfaces and user-observable behavior rather than implementation details.

## Files and Fixtures

- Place test files next to the target file as `*.test.ts(x)` or in a nearby `__tests__/`.
- If fixture values are magic values, keep them as named constants inside the test file.
- Split large fixtures into builders or fixture factories.
- Use snapshots only when the structure is stable and reviewable.

## Mocks

- Mock only uncontrollable boundaries such as external systems, time, randomness, native bridges, and networks.
- Do not mock pure functions or domain logic in the same process.
- Clean up timers, intervals, listeners, and subscriptions at the end of tests.
- Async tests must not leave pending promises or open handles.

## Verification

- `pnpm test` must pass before a PR.
- If tests are too slow, isolate the slow cause and split unit tests from integration tests.
