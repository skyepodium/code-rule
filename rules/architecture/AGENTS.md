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
- Services handle side effects and access to external systems.
- Utilities handle only pure calculations without side effects.
- Adapters wrap external boundaries such as frameworks, platforms, SDKs, and native bridges.
- Models and types express domain meaning and avoid unnecessarily pulling in UI or SDK implementation types.

## Dependency Direction

- Higher layers call lower layers. Lower layers do not import screens, routers, or framework entries.
- If circular dependencies appear, move common types, pure utilities, or adapter interfaces to a lower layer.
- Do not spread SDK objects directly across the app. Wrap only the needed functionality in service/adapter functions.
- Collect platform/framework conditionals in boundary modules when possible. Call sites should use meaningful function names.

## File Size and Split Criteria

- Each file has one role.
- Treat files over 600 LOC as split candidates.
- Split a file when different reasons for change, such as state, gestures, playback, navigation, permissions, or storage, are mixed together.
- Split in small steps without behavior changes. First establish regression criteria through tests or existing behavior checks.

## Global State

- Do not create new global mutable singletons.
- If process-level state is needed, contain it within a service boundary and explicitly define lifecycle, reset, and cleanup APIs.
- Global state that cannot be initialized in tests is a design smell.
- Caches, queues, and listener registries must reveal expiration, release, and duplicate-registration prevention rules in code.

## Control Flow

- Prefer guard clauses and early returns to keep the happy path shallow.
- Return near the start of a function for failure, missing permission, missing data, platform exclusion, and disabled/no-op conditions.
- Do not hide many conditions in one long boolean. Give domain-meaningful conditions helper names.
