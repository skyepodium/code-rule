# React Rules

This directory defines React component, hook, and effect rules.

## Components

- Components focus on screen composition, display state, and user input wiring.
- Write React components as `const ComponentName = (props: Props) => {}` and place exports below.
- Explicitly type props, and use positive names for boolean props.
- Do not put business rules, API implementation details, or storage access directly inside components.
- Split repeated UI states into small components, but consider hooks or view models when props become excessive.

## Hooks and Effects

- Hooks connect the UI lifecycle to service calls.
- Use `useEffect` only for synchronization with external systems. Do not use it for derived state that can be calculated during render.
- Effects must specify cleanup. Release or cancel timers, subscriptions, listeners, and requests.
- Do not disable lint to hide dependency arrays.
- Use functional updates when state updates depend on previous state.

## State

- Do not mix server data, form state, view state, and global state.
- Do not duplicate values calculable from props into separate state.
- Reflect loading, disabled, and error states in user behavior and accessibility state.
