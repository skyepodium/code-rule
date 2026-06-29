# Responsive Layout Rules

This directory defines screen size, safe area, and overflow rules.

## Layout

- Use fixed width/height only for fixed-format UI, and include responsive constraints.
- Manage screen padding, gaps, and breakpoints with design tokens.
- Consider safe areas, notches, status bars, and navigation bar regions.
- Design screens with keyboards so input fields and submit buttons are not obscured.

## Text

- Ensure text does not overflow its container or cover other UI.
- Consider long words, translated strings, and dynamic type.
- Do not adjust font size directly in proportion to viewport width.

## States

- Avoid excessive layout shift in loading, empty, and error states.
- Ensure hover/focus/pressed states do not change element size.
