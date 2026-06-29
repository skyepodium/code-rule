# Design Token Rules

This directory defines UI visual values and design system token boundaries. In target projects, place it in the closest directory with UI code, such as `src/`, `app/`, `features/`, or `components/`.

## Basic Rules

- Manage colors, spacing, radius, typography, elevation, opacity, z-index, and component dimensions as design tokens.
- Do not declare hex colors, `rgba(...)`, font size, spacing, radius, or opacity values directly in UI components.
- Place tokens in `src/shared/design/tokens.ts` or a platform-specific design token boundary.
- Token files express the product UI language and must not be mixed with domain constants such as API paths, storage keys, or timeouts.

## Token Categories

- Use role-based names for colors, such as `COLOR_TOKENS`. Examples: `SURFACE_PANEL`, `CONTENT_PRIMARY`, `ACCENT_PRIMARY`.
- Manage spacing with `SPACE_TOKENS`, using meaningful names for screen padding, gaps, and compact spacing.
- Manage radius with `RADIUS_TOKENS`.
- Manage typography with `TYPOGRAPHY_TOKENS`, using names that include units.
- Manage fixed dimensions for specific components with `COMPONENT_TOKENS`.

## Call-Site Rules

- Components import and use tokens.
- Do not alias token values again inside components or redefine them with names that blur meaning.
- If the same number has different meanings, use different tokens. For example, even if screen gap and button padding are both `16`, do not combine them into one token.
- When adding a temporary visual value, create a token first and then use it.
- Themeable chrome must receive and propagate a theme object or token set through the view/component tree. Do not leave child tabs, panes, dividers, headers, or hover states pinned to raw base tokens after the parent becomes theme-aware.
- Keep theme tokens role-based, not screen-specific. Prefer roles such as active tab background, divider, muted text, active indicator, and hover background over names tied to one component implementation.

## Platform-Specific UI

- If platform-specific UI exists, such as React Native, Android native, or iOS native, provide token boundaries for each platform.
- Do not write colors or dimensions directly in native UI either. Use the platform language's token object or resources.
- When cross-platform tokens and native-only tokens diverge, keep their names and roles aligned.

## Forbidden Patterns

- Do not write colors directly in components, such as `style={{ color: '#ffffff' }}`.
- Do not write visual values directly in styles, such as `fontSize: 16`, `borderRadius: 8`, or `opacity: 0.72`.
- Do not put design tokens and business constants together in `constants.ts`.
