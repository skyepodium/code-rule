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

## UIKit Objects Owned by SwiftUI

A `UIViewRepresentable` coordinator is short-lived: SwiftUI creates and destroys it
whenever the surrounding view's identity or state changes, which during a scroll or a
gesture can be many times. A `UIView` handed back from `makeUIView` usually is not — it
belongs to whatever model object created it.

- Gesture recognizers, delegates, and observers attached to a long-lived view are owned by
  whatever owns that view, installed once and never withdrawn. A coordinator may add and
  remove itself as a *target*; it must not add and remove the recognizer.
- Detaching a recognizer from a view that is on screen, or removing a target from one that
  is mid-gesture, can leave UIKit's delayed-touch bookkeeping holding a nil where a
  responder belongs, and the process aborts inside event delivery. `deinit` is the worst
  place to do either, because it runs at a moment the framework did not choose.
- The same reasoning covers KVO observations, `NotificationCenter` tokens, and display
  links: register where the lifetime is, borrow only the callback.
- One `UIView` has one superview. A view that a card and a full-screen surface both want
  to show cannot be in both, and moving it mid-animation plays the animation against a
  hole. Render a snapshot in the place that is not authoritative.

## Verification on iOS

- A compile is not a check, and a passing unit suite is not a check for anything visible.
- **The simulator is driven from a shell.** An XCUITest target run by `xcodebuild test`
  presses controls, types, scrolls, reads labels, and attaches screenshots without an Xcode
  window and without any GUI automation. Test any belief that a check needs a GUI against
  this before acting on it.
- A launch argument reaches a screen cheaply; it does not replace pressing the control,
  because what happens on press is usually the subject. Remove one-off diagnostic arguments
  before finishing; a launch argument owned by a committed test is a supported fixture and
  may stay behind `#if DEBUG`.
- Device-only failures are reproduced on the device with the real content that triggers
  them. A blank page is not evidence about a content-dependent WebKit defect.
- Pair an unexpected test-run termination with the device's newest crash report before
  naming a cause. A lost connection says the process disappeared; the exception reason and
  backtrace say why.
- Device identifiers, team identifiers, and signing details stay in local commands and are
  never committed.

## Deployment

- Record bundle ID, signing, and provisioning changes as separate risks.
- Design background execution only within modes Apple allows.
