# Constants and Magic Value Rules

This directory defines rules that forbid magic numbers and magic strings and manage them as domain constants. In target projects, place it under `src/shared/constants/` or another constants directory.

## Basic Rules

- Split all magic numbers and domain magic strings into constants.
- Place constant files under `src/shared/constants/<domain>.ts`.
- Split files by domain. Examples: `viewport.ts`, `pagination.ts`, `route.ts`, `animation.ts`.
- Do not put every value into a single `constants.ts`.
- Do not write timeouts, intervals, animation durations, spring configs, gesture thresholds, hit slop, retry counts, page sizes, cache TTLs, vibration patterns, storage keys, route paths, event names, query keys, permission keys, or header keys directly at call sites.
- If a value is meaningful but only local to one function, assign it to a named local constant instead of leaving the raw expression inline.
- If a value is reused, shared across files, externally meaningful, or part of a domain contract, move it to a domain constants file.
- Prefer adding a clear constant over relying on comments to explain a raw value.

## Naming Rules

- Use `SCREAMING_SNAKE_CASE` for global constants.
- Include units in the name when applicable.
- Use `_PX` for pixels, `_MS` for milliseconds, `_RATIO` for ratios, `_COUNT` for counts, and `_LENGTH` for lengths.
- Use `_SECONDS` for second values, `_MINUTES` for minute values, and `_BYTES` for byte values.
- Values with boolean meaning must use positive names.

## Object Constants

- When three or more constants are strongly related, group them into a feature-level object.
- Object names must reveal the domain and role.
- Internal keys must also keep `SCREAMING_SNAKE_CASE` and units.
- Make objects immutable with `Object.freeze` or `as const`.

```ts
const VIEWPORT_TOOLTIP = Object.freeze({
  OFFSET_X_PX: 12,
  OFFSET_Y_PX: -28,
  FONT_SIZE_PX: 12,
});

export { VIEWPORT_TOOLTIP };
```

## Call-Site Rules

- Call sites must access constants with clear meaning, such as `VIEWPORT_TOOLTIP.OFFSET_X_PX`.
- Do not blur meaning with aliases when importing constants.
- Constantize a value when intent matters, even if it is used in only one place.
- Prefer a named variable for intermediate calculations when it makes the next line read like business logic.
- Keep test fixture values as named constants inside the test file.

## Acceptable Inline Values

- Language-idiomatic values such as `0`, `1`, and `-1` may be allowed narrowly in lint configuration.
- Judge empty strings, boolean literals, `null`, and `undefined` by type and domain meaning rather than the magic value rule.
- CSS class tokens follow the `classnames` rules.
- Visual values such as colors, spacing, typography, radius, and opacity follow the design token rules.
- HTTP methods, route paths, storage keys, event names, and query keys are domain strings and must be constantized.

## Forbidden Patterns

- Do not inline time values like `setTimeout(callback, 300)`.
- Do not inline size values like `style={{ width: 320 }}`.
- Do not write storage keys or header keys like `"user-id"` directly at call sites.
- Do not copy the same number to multiple places. If two values happen to be the same but have different meanings, use different constants.
