# API Rules

This directory defines HTTP/API client, schema validation, and retry rules.

## Boundaries

- Keep API calls at adapter or service boundaries.
- UI components must not directly handle fetch implementation details, headers, or raw endpoints.
- Constantize endpoint paths, header keys, query keys, and timeouts.
- Explicitly type requests/responses, and validate external responses before converting them to domain types.

## Failure Handling

- Distinguish network errors, timeouts, authentication failures, and validation failures.
- Apply retries mainly to idempotent requests, and constantize retry counts/backoff.
- Centralize authentication refresh and retry flows in one boundary instead of duplicating them.

## Data Models

- Do not mix API DTOs with UI view models.
- Handle the possibility of unknown server enum/string union values.
- Separate parsing and formatting boundaries for dates, numbers, currency, and units.
