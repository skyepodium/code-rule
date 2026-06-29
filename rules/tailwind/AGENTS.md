# Tailwind Rules

This directory defines Tailwind class and token usage rules.

## Writing Classes

- Use `classnames` or the project's standard `cn` wrapper for conditional class composition.
- Use arbitrary values only as one-off exceptions absent from design tokens, and leave the reason.
- Split long `className` values into meaningful components or variant helpers.

## Tokens

- Align colors, spacing, radius, and typography between Tailwind config and design tokens.
- Do not write raw hex colors directly as arbitrary values in `className`.
- Variant names should reveal meaning rather than visual values.

## Forbidden

- Do not compose className with conditional template literals.
- Do not duplicate the same visual value in both Tailwind classes and inline styles.
