# React Native Rules

This directory defines React Native app, platform branch, and native bridge rules.

## Structure

- `App.tsx`, `index.js`, and native app delegate/activity are responsible only for bootstrap and wiring.
- Isolate direct native bridge access in adapters.
- Wrap platform side effects such as permissions, AppState, Linking, DeviceEventEmitter, and NativeModules at service or adapter boundaries.
- Collect platform branches in `*.ios.ts`, `*.android.ts`, or platform adapters when possible.

## UI

- Use design tokens for visual values.
- Use `StyleSheet.create` by default, and keep inline styles only for narrow cases requiring dynamic values.
- Review touch target, safe area, keyboard avoidance, and text overflow by default.
- Design lists with virtualization in mind when data size can grow.

## Native Integration

- Constantize native module names, event names, and permission keys.
- Native listener registration must prevent duplicate registration and provide cleanup APIs.
- Manage bridge payloads together with TypeScript types and native parsing boundaries.
- Hide Android/iOS native implementations behind adapters so they do not break the JS service contract.
