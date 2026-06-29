# Android Rules

This directory defines rules for Android native code and configuration.

## Manifest and Permissions

- When adding a permission, implement the usage purpose and user guidance flow together.
- Explicitly set the `exported` value for activities, services, and receivers.
- Foreground services must have a notification channel and a stop path.
- Special permissions must include a flow that rechecks state after moving to the settings screen.

## Kotlin/Java

- Android entry points are responsible only for wiring.
- Split business logic into services, managers, or adapters.
- Use native tokens/resources, and do not write colors or dimensions directly in views.
- Release listeners, callbacks, handlers, and runnables in the lifecycle.

## Resources

- Use lowercase snake_case for resource names.
- Split strings into resources when possible, but keep bridge contract keys as constants.
- Check density-specific assets and adaptive icon requirements.
