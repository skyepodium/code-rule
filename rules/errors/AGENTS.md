# Error Handling Rules

This directory defines error model, user message, and logging boundary rules.

## Basic Principles

- Treat `catch` values as `unknown` and use them only after narrowing.
- Empty `catch` blocks are forbidden. Specify one of recovery, logging, retry, or rethrow.
- Separate user-facing messages from developer log messages.
- Convert external system errors into domain errors at service/adapter boundaries.

## User Messages

- User messages must be short and actionable.
- Do not put sensitive internal information, stack traces, tokens, or raw responses in user messages.
- Manage message strings as domain-specific message maps or constants.

## Recovery and Retry

- Constantize retry counts, backoff, and timeouts.
- Apply retries only to idempotent work or clearly safe work.
- Reveal the intent of fallbacks that swallow failures through comments or code structure.

## Error Code Taxonomy

- Errors that code, gates, or tests branch on carry a stable machine-readable code drawn from a documented closed set, separate from the human-readable message.
- Shape codes as `<domain>_<condition>` and extend the field reference when the failure points at a specific field.
- Never branch on message text. Substring matching against prose makes a reworded message a behavior change; use a typed error class or the code instead.
- Give an expected failure an actionable message that names the next step, including the exact command or field to fix.
- Distinguish absence from violation. A missing optional artifact may return a falsy value, but a contract violation must raise; collapsing both into "not ready" hides the violation.

