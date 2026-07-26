# Responsive Layout Rules

This directory defines screen size, safe area, and overflow rules.

## Layout

- Use fixed width/height only for fixed-format UI, and include responsive constraints.
- Manage screen padding, gaps, and breakpoints with design tokens.
- Consider safe areas, notches, status bars, and navigation bar regions.
- Design screens with keyboards so input fields and submit buttons are not obscured.
- Distinguish physical viewport bounds, content-safe bounds, and platform UI risk regions. Do not label one rectangle simply as the safe area when it represents only one of these concepts.
- Treat platform overlay estimates as conservative guidance unless the platform publishes a stable guarantee. Verify important content in the real target surface.
- Keep layout guides out of production output. Preview-only overlays need an explicit render-exclusion mechanism and a regression check.

## Text

- Ensure text does not overflow its container or cover other UI.
- Consider long words, translated strings, and dynamic type.
- Do not adjust font size directly in proportion to viewport width.
- Measure translated text with the production font and available safe width. Character counts and source-language line breaks are not portable layout rules.

## States

- Avoid excessive layout shift in loading, empty, and error states.
- Ensure hover/focus/pressed states do not change element size.
