# Native Desktop App Rules

This directory defines rules for desktop apps that ship as native app bundles or mix UI code with a native core, renderer, plugin, or dynamic library. In target projects, place it near the app root or native frontend directory, such as `Sources/`, `App/`, `macos/`, `desktop/`, or the directory that owns app packaging.

## Platform Boundaries

- Keep platform UI, lifecycle, menus, windows, notifications, pasteboard, input methods, shell/process handling, and bundle integration in the platform app layer.
- Keep portable terminal, parser, protocol, storage, rendering model, and business/domain logic outside the platform UI layer when the codebase has a native core or shared engine.
- Cross-language contracts must be explicit. C ABI functions, FFI structs, shader buffer layouts, serialized settings, and native bridge payloads require matching tests or documented verification when changed.
- Do not let lower-level native cores import app UI frameworks. Platform adapters may call the core; the core should expose stable project-owned APIs.
- Keep native handles, file descriptors, process IDs, observers, timers, GPU resources, and dynamically loaded libraries behind owners with cleanup paths.

## App Bundle Versus Development Executable

- Treat a raw development executable and an installed app bundle as different runtime contexts.
- User-visible desktop behavior that depends on OS identity, activation, input methods, notifications, app icons, entitlements, resources, or dynamic library lookup must be verified against the installed app bundle.
- A development command such as `swift run`, `cargo run`, or a debug executable is useful for fast iteration, but it does not prove bundle behavior.
- Packaging scripts must copy required resources, frameworks, plugins, shaders, dynamic libraries, icons, and metadata into the final app bundle through reproducible commands.
- If the app changes resource lookup or native library loading, verify both development fallback paths and installed-bundle paths.

## Input Methods And Text

- Let the platform text input system own IME composition. Do not manually compose language-specific preedit text, normalize partial input, or synthesize replacement text unless there is a documented platform contract and regression evidence.
- Text sent to shells, documents, editors, or other backends must come from confirmed text callbacks or explicit control-key handling, not raw key characters that may belong to IME composition.
- Preedit or marked text is visual state. Display it without committing it to the persistent model or backend output.
- Input-method regressions require event-flow evidence from the installed app when possible, including key events, preedit updates, committed text callbacks, focus changes, and backend writes.

## Rendering And Native Resources

- Renderer state should follow a model-owned source of truth. Do not infer protocol or document semantics from pixels, screenshots, literal placeholder text, or one specific app's output.
- GPU buffers, textures, glyph atlases, font caches, and native render passes need stable ownership, invalidation rules, capacity limits, and release paths.
- Rendering fixes need targeted regression coverage for the model/protocol state that caused the visual bug, plus visual or bundle-level evidence when the issue is user-visible.
- Keep shader structs and host-side buffer layouts synchronized. Any layout change must update both sides and include a verification gate.

## Packaging And Verification

- Package metadata such as bundle identifier, version, display name, icon file, minimum OS, entitlements, update feed, and signing configuration must come from explicit constants, manifests, or scripts.
- Install/package scripts should fail before reporting success when required resources, icons, signatures, native libraries, or metadata are missing.
- Release artifacts must be reproducible from source inputs. Do not regenerate canonical assets from previously generated installed bundles, screenshots, caches, or manually copied outputs.
- Before claiming a desktop app fix is complete, run the smallest relevant unit/integration test, then the app's package or install verification when the behavior depends on the final bundle.
