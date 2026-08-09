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

## Reads a Declarative Framework Can Reach

A declarative renderer re-evaluates whenever it likes: mid-dismissal, mid-animation, after
one mutation and before the next. Any window in which two pieces of state disagree is a
window a user can land in, and the framework will happily read through it.

- A selector, computed property, or derived value the view layer can reach must not throw
  and must not assert. Crashing on an inconsistent snapshot is for bugs that cannot ship,
  not for a state the renderer can legitimately observe between two of its own passes.
- Return an empty, neutral, or explicitly absent value instead. The screen a user sees for
  one frame while the state settles is a design question, not a reason to abort.
- State that must agree is changed by one function, never by two assignments that a render
  can interleave.
- Decoded input — restored sessions, cached payloads, anything out of local storage — is
  untrusted. Validate and degrade it; never let it index into a collection unchecked.
