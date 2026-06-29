# Config Rules

This directory defines environment variable, runtime config, and feature flag rules.

## Environment Variables

- Env names must use uppercase English letters and `_`.
- Distinguish public client env prefixes from private server env prefixes.
- Record required keys and their meaning in `.env.example` or documentation.
- Validate env values at the startup boundary and convert them to typed config.

## Runtime/Build Config

- Do not mix build-time config with runtime config.
- Split platform-specific config into adapters or platform config files.
- Constantize config defaults and do not create hidden fallbacks.

## Feature Flags

- Document each flag's name, owner, and removal condition.
- Specify removal timing for temporary flags.
- Collect flag branches in boundary components or services when possible.
