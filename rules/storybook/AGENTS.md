# Storybook Rules

This directory defines component story and visual documentation rules.

## Story Scope

- Reusable UI components must have stories for default, loading, disabled, error, and empty states.
- Form controls must include validation/error/focus states.
- If design tokens or themes change, verify them with representative stories.

## Writing

- Story args must match the actual props type.
- Manage mock data as named fixtures.
- Do not put API calls or production side effects inside stories.

## Verification

- For visual regression stories, freeze volatile time, randomness, and animations.
- Check basic labels/roles with an accessibility addon or manual checks.
