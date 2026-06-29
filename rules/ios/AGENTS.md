# iOS Rules

This directory defines rules for iOS native code and configuration.

## Info.plist and Permissions

- Permission usage descriptions must clearly explain the feature purpose.
- When adding entitlements, background modes, or capabilities, document the need and deployment impact.
- Do not rely on private APIs.

## Swift/Objective-C

- AppDelegate/SceneDelegate are responsible only for bootstrap and wiring.
- Split native bridges into small modules and specify the JS contract.
- Clean up threads, callbacks, and observers according to the lifecycle.
- Use UI visual values through token/resource boundaries.

## Deployment

- Record bundle ID, signing, and provisioning changes as separate risks.
- Design background execution only within modes Apple allows.
