# ESLint Rules

This directory defines ESLint configuration and lint scope rules. In target projects, place it at the root or in the directory that contains lint configuration files.

## Required Checks

- `pnpm lint` must pass before a PR.
- TypeScript projects must also pass `pnpm typecheck`.
- Limit lint targets to directly managed app source and configuration files.
- Exclude `dist`, `build`, `.next`, `coverage`, `node_modules`, and generated files from lint targets.

## Required Rule Intent

- Forbid function declarations and enforce arrow function expressions.
- Forbid `any`.
- Forbid introducing magic numbers and magic strings.
- Forbid unused variables and unused imports.
- Enforce React hook rules.
- Keep import order and type-only imports consistent.

## Recommended Rule Shape

```js
{
  "func-style": ["error", "expression", { "overrides": { "namedExports": "expression" } }],
  "prefer-arrow-callback": "error",
  "@typescript-eslint/no-explicit-any": "error",
  "@typescript-eslint/no-unused-vars": "error",
  "@typescript-eslint/consistent-type-imports": "error",
  "no-magic-numbers": "off",
  "@typescript-eslint/no-magic-numbers": [
    "error",
    {
      "ignore": [0, 1, -1],
      "ignoreArrayIndexes": true,
      "ignoreEnums": false,
      "ignoreReadonlyClassProperties": false
    }
  ]
}
```

## Disable Comments

- `eslint-disable` is a last resort.
- Immediately above the disable, write the reason and removal condition in English.
- File-wide disables are forbidden. If they are truly necessary, split them into a separate issue or PR.
- Put generated files in the ignore scope instead of disabling lint.

## Next.js Projects

- Layer team rules on top of the official Next lint configuration or the project's standard flat config.
- Keep exceptions required by App Router file conventions narrow and scoped by file glob.
- When relaxing lint rules, leave examples of the code patterns that require it.
