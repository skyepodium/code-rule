# Expo Rules

This directory defines Expo managed, prebuild, and EAS rules.

## Project Mode

- First distinguish managed workflow requirements from bare/prebuild requirements.
- If native custom code is needed, specify a config plugin or prebuild strategy.
- Document whether `ios/` and `android/` are generated and who owns them.

## Configuration

- Manage app config values in typed config or a clear config file.
- Validate permissions, schemes, intent filters, and associated domains together with config plugins or native configuration.
- Distinguish env and build type by EAS profile.

## Dependencies

- Check Expo SDK version and React Native version compatibility.
- When adding a native module, specify whether Expo Go supports it.
