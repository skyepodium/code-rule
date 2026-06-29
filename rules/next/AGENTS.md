# Next.js Rules

This directory defines rules for Next.js App Router projects. In target projects, place it under `app/` or `src/app/`.

## Routing Model

- Use App Router by default.
- Do not mix the `pages/` router with App Router for new features.
- `page.tsx` handles screen composition, `layout.tsx` handles common layout, and `route.ts` handles only HTTP boundaries.
- `loading.tsx`, `error.tsx`, and `not-found.tsx` handle only state UI for the corresponding segment.

## Server Components and Client Components

- Use server components by default.
- Place `"use client"` only on the smallest leaf component that needs interaction, browser APIs, or React state/effects.
- Client component props must be serializable values.
- Separate server-only code, secrets, and database clients so they do not enter the client bundle.
- Place providers as deep as possible to broaden the static server rendering scope.

## Data Access

- Fetch data that can be fetched on the server from server components, server actions, or route handlers.
- Do not handle external API secrets directly on the client.
- Declare `fetch` cache, revalidate, and runtime settings as top-of-file constants, and do not leave magic numbers.
- Explicitly type requests and responses, and validate external responses before use.

## Route Handlers

- Route handler files must be named `route.ts`.
- Use arrow function expressions such as `export const GET = async (...) => {}` instead of function declarations.
- Do not use `NextApiRequest` or `NextApiResponse` in App Router route handlers.
- Constantize response status codes, cache TTLs, and header names.
- If one file contains multiple HTTP methods, split common logic into pure functions.

## Metadata and SEO

- Put static metadata in a `metadata` export.
- Write dynamic metadata with `generateMetadata` as an arrow function expression.
- If title, description, or Open Graph strings repeat, split them into constants or config.

## Built-In Next Components

- Use `next/link` for internal navigation.
- Prefer `next/image` for images that need optimization.
- Fonts must follow Next font or the project's standard loading path.
