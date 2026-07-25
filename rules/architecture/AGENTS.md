# Architecture and Responsibility Boundary Rules

This directory defines project structure, entry points, side-effect boundaries, and file responsibilities. In target projects, place it in the closest directory that composes execution flow, such as the app root, `src/`, `app/`, or `features/`.

## Entry Points

- Keep entry points as thin as possible.
- `main.ts`, `index.tsx`, `App.tsx`, root provider, root router, native app delegate/activity, and server entry are responsible only for bootstrap and wiring.
- Do not calculate business rules directly in entry points.
- Split implementation details such as networking, storage, notifications, authentication, payments, native bridges, and analytics into services or adapters.
- Entry points should only compose initialization order, provider wiring, router wiring, global listener registration, and top-level error boundary wiring.

## Responsibility Boundaries

- UI components focus on screen composition, display state, and user input wiring.
- Hooks connect the UI lifecycle to domain/service calls.
- Controllers, route handlers, screen event handlers, and command handlers translate protocol/UI input into use-case calls and map results back to responses or view state.
- Services handle side effects and access to external systems.
- Services own business use cases, orchestration, policy decisions, authorization decisions, and transaction boundaries.
- Repositories own persistence queries, storage access, database mapping, and durable data retrieval.
- Utilities handle only pure calculations without side effects.
- Adapters wrap external boundaries such as frameworks, platforms, SDKs, and native bridges.
- Models and types express domain meaning and avoid unnecessarily pulling in UI or SDK implementation types.

## Layered Architecture

- Use strict layer separation for non-trivial features: controller/route/screen boundary -> service/use case -> repository -> adapter/external system.
- Controllers must not contain business rules, storage queries, SDK calls, retry policy, or transaction logic.
- Services must not import UI components, route objects, request/response framework types, or platform-specific view APIs.
- Repositories must not know about UI, routes, controllers, analytics, or user-facing messages.
- Adapters must expose project-owned functions/types instead of leaking raw SDK clients through the app.
- Shared domain types belong below controllers and services so lower layers do not import higher-layer types.
- If a feature does not need a full repository layer, document the simpler boundary and keep the service interface stable enough to add a repository later without changing callers.
- For write flows, keep validation, authorization, persistence, and side-effect publication in named steps rather than one mixed function.

## Dependency Direction

- Higher layers call lower layers. Lower layers do not import screens, routers, or framework entries.
- If circular dependencies appear, move common types, pure utilities, or adapter interfaces to a lower layer.
- Do not spread SDK objects directly across the app. Wrap only the needed functionality in service/adapter functions.
- Collect platform/framework conditionals in boundary modules when possible. Call sites should use meaningful function names.
- Cross-layer imports that skip the service boundary are forbidden unless the lower-level module is a pure domain utility or type.

## Interface Design

- Keep public interfaces smaller than implementations.
- Prefer one clear use-case function over broad service objects with unrelated methods.
- Avoid functions with many positional parameters; use a typed options object when the call is not self-explanatory.
- Return domain results from services, not raw API responses, database rows, SDK objects, or UI-specific state.
- Make failure modes explicit with typed errors, result objects, or documented exceptions at the boundary.
- Views, controllers, and feature code should depend on project-owned protocols or adapters for platform backends such as shells, native handles, storage, rendering devices, push services, and SDK clients. Keep concrete platform implementations replaceable without changing the caller's behavior.

## File Size and Split Criteria

- Each file has one role.
- Treat files over 600 LOC as split candidates.
- Split a file when different reasons for change, such as state, gestures, playback, navigation, permissions, or storage, are mixed together.
- Split in small steps without behavior changes. First establish regression criteria through tests or existing behavior checks.
- Split earlier when one file mixes controller mapping, service orchestration, repository access, formatting, validation, and UI state.
- Treat a function with many branches, many parameters, or nested control flow as a split candidate even if the file is still small.

## Global State

- Do not create new global mutable singletons.
- If process-level state is needed, contain it within a service boundary and explicitly define lifecycle, reset, and cleanup APIs.
- Global state that cannot be initialized in tests is a design smell.
- Caches, queues, and listener registries must reveal expiration, release, and duplicate-registration prevention rules in code.
- Long-lived in-memory collections must have ownership, eviction, and cleanup rules.
- Do not retain large objects, raw responses, blobs, native handles, or DOM references beyond the lifecycle that needs them.

## Control Flow

- Prefer guard clauses and early returns to keep the happy path shallow.
- Return near the start of a function for failure, missing permission, missing data, platform exclusion, and disabled/no-op conditions.
- Do not hide many conditions in one long boolean. Give domain-meaningful conditions helper names.

## Boundary Enforcement

- A documented import ban that no test checks is a suggestion. Every layer rule stated in a document gets a scan test that walks that layer's source files and fails on a forbidden import.
- Enumerate layer membership in exactly one place and assert both directions: every module belongs to exactly one layer, and every named module still exists. A new module with no declared layer is a layout violation, not a detail to settle in review.
- When the enumeration is a copy of a document, add a test that the two agree. Duplicated contracts drift silently otherwise.
- Record known violations as a named allowlist with a comment pointing at the document that tracks the debt, plus a reverse test that fails when an allowlisted violation no longer exists. A paid-off debt must be deleted, not left as a permanent exemption.
- Prefer a scan test over a lint plugin when the rule is project-specific. It is cheaper to write, easier to read, and fails with a message that names the fix.

## Single Source of Truth and Drift

- A schema field list, state transition, threshold, path rule, taxonomy, or policy has exactly one owning definition. Consumers import it; they do not restate or locally reinterpret it.
- Derive values that can be derived. Do not add a field for something already computable from an existing field, and record the derivation next to it.
- When duplication cannot be avoided across a language, runtime, or process boundary, name one side the authority. The other side is verified against a fixture generated by the authority.
- Check the fixture's own freshness. A stale fixture makes the cross-boundary check pass while the two implementations actually disagree, which is worse than having no check.
- Any file that derives from another is produced by a generator that also offers a non-mutating check mode, and that check runs in the standard verification sequence.
- Extending a shared contract file past its size budget is a signal to split by contract family, not to keep appending. Split before adding more, and verify no export is dangling, duplicated across the new modules, or missing from the public surface.

## Registries and Variant Lifecycle

- Add a variant as data — a registry entry, strategy table, or schema record — never as another branch in a conditional chain. If adding a variant requires editing three functions, refactor to a table first.
- Load a long-lived registry through a schema-validating loader with a version field and field-precise error messages.
- Retire a registry entry by status, not deletion. Flip it to a deprecated state and point at its replacement, so existing data referencing the old name still resolves.
- Keep the closed set of valid values in the registry's own module and validate against it at the boundary.

## Utility Module Naming

- Name a shared module for the capability it owns. `utils`, `helpers`, `common`, `misc`, and `shared` are forbidden filenames; they become dumping grounds and their contents acquire no owner.
- A wrapper that tolerates a failure documents in its docstring or header comment exactly which failures it swallows and confirms that every other failure stays fatal.
- Do not create a shared abstraction because two blocks look similar. Extract when inputs, outputs, errors, and reasons to change genuinely match.
