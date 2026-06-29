# Form Rules

This directory defines form state, validation, and submit rules.

## State

- Distinguish field value, touched, dirty, error, and submit state.
- Use a validation schema or explicit validators.
- Distinguish server validation errors from client validation errors.
- Do not put form state in a global store unnecessarily.

## Inputs

- Do not mix the roles of input labels, placeholders, helper text, and error text.
- Separate parsing from display formatting for numbers, dates, currency, and phone numbers.
- Consider IME composition and mobile keyboard types.

## Submit

- Prevent duplicate submit execution.
- On submit failure, provide a message users can recover from.
- Specify criteria for reset, navigation, and optimistic updates after success.
