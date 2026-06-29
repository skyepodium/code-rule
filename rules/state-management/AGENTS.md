# State Management Rules

This directory defines local, server, and global state boundaries.

## State Classification

- Distinguish local view state, form state, server state, and global app state.
- Do not duplicate data that can be fetched again from the server into a global store.
- Calculate values derivable from props or other state as derived state.
- Do not hide state that should be owned by the URL/route inside a component.

## Store

- Split stores into small slices and modify them only through public actions.
- Use selectors to reduce unnecessary re-renders.
- Do not store SDK objects, navigation objects, or React components in stores.
- Explicitly define reset/cleanup APIs so tests and logout flows can initialize state.

## Side Effects

- Do not hide side effects inside stores; split them into service/action boundaries.
- Design optimistic updates together with rollback conditions and failure messages.
