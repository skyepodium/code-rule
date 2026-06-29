# State Management Rules

This directory defines local, server, and global state boundaries.

## State Classification

- Distinguish local view state, form state, server state, and global app state.
- Do not duplicate data that can be fetched again from the server into a global store.
- Calculate values derivable from props or other state as derived state.
- Do not hide state that should be owned by the URL/route inside a component.
- Every state value must have one explicit owner and one reset/lifecycle policy.
- Server state belongs in the server-state/cache layer, not in ad hoc global stores.
- URL/route state owns shareable navigation state; forms own draft input; local view state owns transient presentation state.

## Store

- Split stores into small slices and modify them only through public actions.
- Use selectors to reduce unnecessary re-renders.
- Do not store SDK objects, navigation objects, or React components in stores.
- Explicitly define reset/cleanup APIs so tests and logout flows can initialize state.
- Do not store raw API responses, database rows, large blobs, DOM nodes, native handles, promises, or subscriptions.
- Store actions may call services, but stores must not reach directly into repositories, SDK clients, or raw storage.
- Global store slices must remain independently testable and removable.

## Side Effects

- Do not hide side effects inside stores; split them into service/action boundaries.
- Design optimistic updates together with rollback conditions and failure messages.
- Keep cross-slice orchestration in services or named use cases rather than implicit subscriptions between stores.
- Cleanup for optimistic, cached, or subscribed state must be explicit on logout, account switch, workspace switch, and test reset.
