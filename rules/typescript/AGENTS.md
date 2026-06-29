# TypeScript Rules

This directory defines TypeScript and React TypeScript code rules. When copying it to a target project, place it in the closest directory with TypeScript code, such as `src/`, `app/`, `lib/`, or `components/`.

## Type Safety

- `any` is forbidden. Accept values as `unknown` and narrow them when needed.
- Convert external input to domain types through schema validation or explicit narrowing.
- Explicitly type public exported functions and React component props.
- `as` assertions are a last resort. When used, the code structure must show why they are safe.
- Non-null assertions with `!` are forbidden. Narrow with branches, guards, or early returns.

## Function Expressions

- Function declarations are forbidden.
- Regular functions use arrow function expressions in the form `const functionName = (...) => {}`.
- React components also use `const ComponentName = (props: Props) => {}` and place exports below.
- Hooks use the form `const useThing = (...) => {}`.
- If overloads are required, separate the type alias from the implementation function.

## Control Flow

- Use guard clauses and early returns actively.
- Return quickly near the start of the function for failure, missing permission, missing data, platform exclusion, and disabled/no-op conditions.
- Avoid `else` after `return`, `throw`, `continue`, or `break` so the happy path has less indentation.
- If an early return condition contains domain knowledge, reveal its meaning with a boolean helper or named constant.
- Do not hide multiple conditions on one line. Split independent failure conditions in readable order.

## Imports and Modules

- Prefer `~/...` absolute paths for imports.
- Allow `./file` relative paths only for files inside the same folder.
- Configure the `~/...` alias consistently not only for TypeScript but also for bundler, test runner, native/metro/vite/webpack configuration.
- When adding absolute-path imports to a project without alias configuration, first add the configuration and verification together.
- Use `import type` for type-only imports.
- Do not create circular dependencies. If they occur, move common types or pure utilities to a lower layer.
- Forbid top-level mutable singletons in modules. Inject services through arguments, props, context, or factories.

## Error Handling

- Treat values caught in `try/catch` as `unknown`.
- Use messages and causes only after `instanceof Error` or explicit guards.
- Empty `catch` blocks are forbidden. Recover, log, or rethrow.
- Manage UI-exposed error messages as domain-specific constants or message maps.

## File Boundaries

- Each file has one role.
- Consider splitting files over 600 LOC.
- React component files contain only the component, props type, and small render helper functions.
- Extract business logic into pure functions and isolate side effects in service or adapter modules.
