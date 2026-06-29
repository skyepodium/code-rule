# Logging and Observability Rules

This directory defines logging, analytics, and crash reporting rules.

## Logging

- Do not leave arbitrary `console.log` calls in production code.
- Use a logger wrapper and specify level, domain, and context.
- Do not log PII, tokens, raw credentials, or sensitive payloads.
- When logging in `catch`, reveal recoverability and user impact together.

## Analytics

- Constantize event names and property keys.
- Analytics events must connect to user behavior or product questions.
- Avoid duplicate events and render-based automatic firing.
- Check consent state for events that require consent.

## Crash/Reporting

- Wire error boundaries and crash reporters at the bootstrap boundary.
- Report non-fatal errors only when they are actionable.
- Send release version, build number, and platform context together.
