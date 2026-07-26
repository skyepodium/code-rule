# Media Editing and Deterministic Rendering Rules

This directory defines rules for applications that edit or render video,
audio, subtitles, canvas animation, thumbnails, or other time-based media. In
target projects, place it near the editor, render pipeline, effect catalog, or
media adapters that it governs.

## Source and Artifact Ownership

- Preserve imported source media. Editing creates a project description and
  derived artifacts; it never rewrites the source in place.
- Treat project data, effect cues, subtitle tracks, and render profiles as
  versioned contracts with schema validation at the loading boundary.
- Keep source time and output time distinct. A timeline module owns the mapping
  between them; renderers and UI controls do not reinterpret clip offsets.
- For frame-accurate work, define interval semantics explicitly, preferably
  half-open ranges `[start, end)`, and derive frame indexes from one declared
  frame rate or rational time base.
- Derived media is never an input to the next edit generation when the original
  source and project description can reproduce it. Re-cropping a rendered
  horizontal export to make a vertical export compounds subtitle, scaling, and
  compression damage.
- Exclude large renders, frame sequences, caches, browser profiles, and
  temporary audio files from source control. Commit the schema, project
  template, renderer, and reproducible command instead.

## Renderer Architecture

- Treat effects, subtitle styles, layouts, and export profiles as data-driven
  variants. Add a registry or schema record before adding another conditional
  branch to the time orchestration loop.
- Separate effect interpretation from effect drawing. One module resolves
  presets, defaults, and project overrides into complete cues; renderer
  adapters consume only resolved cues.
- Keep the timeline orchestrator ignorant of effect-specific DOM, canvas,
  shader, or FFmpeg behavior. Register an adapter when an effect requires new
  rendering behavior.
- A source-video transform such as crop, zoom, stabilization, or blur has one
  production adapter that owns its filter expression. Project scripts and
  services call that adapter instead of rebuilding filter strings.
- Keep preview and export implementations behind the same semantic interface.
  They may use different technologies, but they must consume the same resolved
  cue and implement the same coordinate, timing, easing, and visibility
  contract.
- Test that every registered variant has every required adapter and that no
  adapter exists without a registry entry. Configuration completeness is a
  machine-enforced contract.

## Determinism and Media Time

- Every rendered frame is a pure function of validated project data, source
  media time, and output dimensions.
- Use media time or an explicit frame index for animation. Wall-clock timers,
  CSS animations that advance independently, unseeded randomness, and remote
  assets are forbidden in deterministic export paths.
- Seed procedural layouts in project data and keep the seed stable across
  preview, export, retry, and machine.
- Load and await fonts, images, decoders, and metadata before declaring a
  renderer ready. A DOM-ready page is not necessarily render-ready.
- Provide a frame-render interface that seeks or evaluates one exact time and
  resolves only after the frame is visually complete. Batch export calls this
  interface rather than duplicating editor behavior.

## Coordinate and Geometry Contracts

- Name what a coordinate means: subject anchor, crop origin, crop center,
  transformed position, or output position. A generic `x`/`y` pair is not a
  sufficient interface for persistent media data.
- Store author-facing coordinates in a stable normalized space when practical,
  then convert once at the renderer seam.
- If a zoom parameter names a subject anchor, the authored point in the
  untransformed frame must remain at the same output position during the entire
  zoom. Preview transform origin and production crop math must preserve the
  same invariant.
- Do not copy a CSS transform into an FFmpeg filter by visual analogy. Derive
  both implementations from the coordinate invariant and verify representative
  frames.
- Avoid dynamic filter chains whose downstream geometry is initialized from
  the first frame when upstream dimensions change per frame. Prefer a primitive
  with fixed output geometry or prove the chain with frame-level tests.
- Make crop and focus values editable numerically even when direct manipulation
  is available. Store the values in project data, not as project-specific
  constants inside renderer code.

## Subtitle and Text Effects

- Measure text in the actual render font and output scale. Character counts are
  not a reliable line-breaking rule for Korean, Japanese, mixed Latin text, or
  fallback fonts.
- Declare the font family and weight mapping, ship or provision every required
  glyph, and wait for fonts before both preview and export.
- Render at the target pixel dimensions. Do not capture a low-resolution
  browser preview and upscale it for delivery.
- A cumulative text effect reserves the completed phrase's final footprint from
  the first frame. Earlier segments keep their position, opacity, and transform;
  only the newly introduced segment animates.
- Treat punctuation and separators as authored content or explicit effect data.
  Do not infer final punctuation independently in translation, subtitle, and
  renderer layers.
- Test multilingual text with realistic long strings, font fallback, multiple
  lines, and the exact boundary frames where segments appear or disappear.

## Vertical Video and Safe Areas

- Derive each aspect-ratio version from the source media and shared timeline,
  with its own non-destructive crop, subtitle profile, and effect overrides.
- Distinguish canvas bounds, content-safe bounds, and platform-UI risk regions.
  A dashed guide or shaded region must state which one it represents.
- Treat platform safe-area values as conservative production guidance unless
  the platform guarantees them as a formal specification. UI overlays vary by
  device, locale, account state, and application version.
- Keep essential faces, text, and calls to action inside the intersection of
  supported platforms' conservative safe regions. Decorative content may
  extend outside it.
- Preview guides are editor chrome. Mark them with a render-exclusion mechanism
  and test that export mode hides them.
- Reflow or scale subtitles against the usable safe width. Moving a horizontal
  subtitle unchanged into a vertical canvas is not a layout strategy.

## Color, Alpha, and Image Fidelity

- Declare the working color assumptions and final color tags. Preserve the
  intended transfer, primaries, range, pixel format, and alpha convention
  across browser, image pipe, compositor, and encoder boundaries.
- Verify white, black, brand colors, and semi-transparent edges from frames
  extracted from the final encoded file. A correct browser screenshot does not
  prove the encoded result is correct.
- Do not apply chroma-key cleanup, matte removal, or color conversion to text
  and solid UI layers unless that operation is part of their declared asset
  contract.
- Avoid repeated lossy encode cycles. Composite from the highest-quality
  available source and encode the delivery file once after the edit is final.
- Match the render viewport, screenshot region, device scale factor, and encoder
  dimensions exactly so the pipeline does not introduce an implicit resize.

## Audio Delivery

- Keep mix decisions and delivery mastering separate. Preserve the source mix,
  then apply a named output loudness profile at the final delivery stage.
- Specify integrated loudness, true-peak ceiling, sample rate, channel layout,
  and codec in the output profile. Do not adjust master volume by an unexplained
  multiplier.
- Measure the final encoded file, not only the pre-encode stream. Lossy encoding
  can change true peak and measured loudness.
- Avoid normalization that destroys deliberate dynamics. Use limiting only to
  enforce the declared ceiling, and record any gain applied.

## Export Verification

- A successful encoder exit only proves that a process ended. It does not prove
  visual correctness, timing correctness, or delivery compliance.
- Inspect the final artifact for resolution, display aspect ratio, frame rate,
  exact frame count, duration, pixel format, color metadata, audio codec,
  sample rate, channel count, loudness, and true peak.
- Fully decode the completed file with errors treated as failures.
- Capture visual checkpoints at every effect boundary and at representative
  start, maximum, and recovery states. Compare preview and export at the same
  source time or frame index.
- For fixes involving color, crop, subtitle alignment, font quality, or safe
  areas, verify a frame extracted from the final encoded file. Intermediate
  screenshots are diagnostic evidence only.
- Report the reproducible render command or profile, verification results, and
  any checks that could not run. Do not report a media artifact as complete
  from file existence or casual playback alone.
