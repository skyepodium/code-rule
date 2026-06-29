# Accessibility Rules

This directory defines baseline UI accessibility rules.

## Basics

- Interactive elements must have accessibility labels and roles.
- Icon-only buttons must provide a visible tooltip or an accessibility label.
- Disabled/loading states must be reflected in both visual state and accessibility state.
- Important state changes must have a path that screen readers can perceive.

## Input and Focus

- Form fields must clearly define the relationship between labels, errors, and hints.
- Modals, drawers, and dialogs must have focus traps and close behavior.
- Keyboard navigation order must match the visual order of the screen.

## Visuals

- Check text contrast and manage it with tokens.
- Touch targets must meet the platform-recommended minimum size.
- Motion must respect reduced-motion settings.
