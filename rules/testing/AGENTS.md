# Testing Rules

This directory defines unit, integration, and component test rules.

## Basic Principles

- Add tests first or update existing tests for changed behavior.
- For bug fixes, lock the symptom with a failing regression test before fixing it.
- Test names must describe expected behavior. Do not use meaningless names like `works` or `test1`.
- Tests verify public interfaces and user-observable behavior rather than implementation details.
- Source-shape tests are allowed only as guardrails for architecture boundaries, generated code contracts, or known regression-prone wiring. They do not replace executable behavior tests for user-visible fixes.
- When a source-shape test fails because the implementation improved, update the assertion to preserve the architectural intent instead of freezing old implementation details.

## Files and Fixtures

- Place test files next to the target file as `*.test.ts(x)` or in a nearby `__tests__/`.
- If fixture values are magic values, keep them as named constants inside the test file.
- Split large fixtures into builders or fixture factories.
- Use snapshots only when the structure is stable and reviewable.
- A test that asserts against a fixture proves the fixture. Where a file ships with the
  product - translation catalogs, configuration, schemas, seed data - at least one test
  opens the real file. Catalogs that had silently drifted apart were found this way and by
  nothing else.
- A bug fix ships with a test that fails without it. For anything that decodes stored or
  remote input, feed it the empty case, a reference to something absent, a truncated
  payload, and the wrong version.

## Mocks

- Mock only uncontrollable boundaries such as external systems, time, randomness, native bridges, and networks.
- Do not mock pure functions or domain logic in the same process.
- Clean up timers, intervals, listeners, and subscriptions at the end of tests.
- Async tests must not leave pending promises or open handles.

## Reproducing Before Measuring

- A harness that does not perform the reported trigger is measuring a different defect.
  Write down the trigger as the reporter described it, then check that the harness performs
  it. Ten trials under conditions that exclude the symptom are not weak evidence; they are
  evidence about something else, and the volume makes it look rigorous.
- When the trigger cannot be automated, say so and treat every number as provisional rather
  than quietly substituting a proxy that can be.
- Never report a fix from a run that did not reproduce the symptom.
- When reading the code has produced two or more wrong diagnoses, stop reading and start
  disabling. Turn one variable off at a time and measure. For an intermittent defect,
  measure a rate across repeated runs; a single pass carries no information.
- Pair an unexpected process termination with the platform's own crash report before naming
  a cause. "The process disappeared" and "here is the exception that killed it" are
  different facts.

## Verification

- `pnpm test` must pass before a PR.
- If tests are too slow, isolate the slow cause and split unit tests from integration tests.
- For performance work, include the smallest regression guard that proves the intended allocation, invalidation, or cache behavior, plus a normal build/test gate.
- A compile is not a check, and neither is a green unit suite for a change a person can
  see. Exercise the thing that changed, or report that it was not exercised.

## Contract Locking

- Building a rule and keeping it from silently loosening are separate jobs. Only a regression test does the second.
- Lock the stable interface, not the implementation: public signatures, serialized shapes, error codes, hashes, and deterministic output. A refactor that changes any of them is a contract change and must update the test deliberately.
- When a test asserts the exact contents of a contract surface, treat its failure as a design question, not a chore. Extending a globally emitted contract for a feature most callers do not use is usually the wrong fix.
- Lock documented behavior that lives in prose too: assert the required phrasing is present and that superseded phrasing is absent, so retired guidance cannot creep back.
- Assert on stable error codes rather than message text, so wording can improve without breaking tests.

## Determinism and Evidence

- Verify determinism where you claim it: produce the artifact twice and compare hashes, rather than assuming a renderer is stable.
- Prove causation before attributing a failure. When a failure appears after merging two changes, run a control with one change removed; identical failures mean you did not cause them.
- Read the actual output of a verification run. A process exit code is not the test result when the command was piped through another program, and a completion notification is not evidence that assertions passed.
- Dry-run a change that must land on top of someone else's in-flight work: apply it to a scratch copy of their version, confirm the anchors are present and unique, and run the affected tests there. A verified re-apply recipe beats a described one.

## Generated Artifact Verification

- Verify the delivered artifact, not only the source, intermediate frame, build log, or encoder exit code.
- Define artifact acceptance as measurable structure plus representative content checks. Examples include dimensions, frame count, duration, metadata, hashes, decoded content, and boundary screenshots.
- Fully parse or decode an artifact when partial corruption can hide behind a successful write. A valid header or first frame is insufficient evidence.
- Test temporal behavior at the exact frame before, on, and after a transition boundary. A midpoint screenshot cannot detect one-frame blinking, overlap, or stale state.
- When two adapters claim parity, feed both the same resolved fixture and compare stable observable invariants rather than private implementation strings.
- Re-run post-processing checks after the final transformation. Encoding, minification, packaging, signing, and copying can alter properties that passed earlier.
