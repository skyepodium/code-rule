# Terminal Emulator And Control Protocol Rules

This directory defines rules for terminal emulators, PTY frontends, shell hosts, and applications that parse or emit terminal control protocols. Place it near the parser, terminal state model, PTY adapter, or application layer that consumes protocol events.

## Protocol Parsing

- Parse terminal input as a byte-stream state machine. Preserve incomplete CSI, OSC, DCS, and related sequences across arbitrary read boundaries; a PTY read is not a protocol-message boundary.
- Bound every control-string and parameter buffer. On overflow or invalid input, enter a defined discard/recovery state until a valid terminator instead of retaining unbounded data or silently interpreting a truncated command.
- Preserve protocol structure through classification. Private prefixes, intermediate bytes, final bytes, semicolon-separated parameters, colon subparameters, omitted values, and terminators can change meaning and must not be flattened before the consumer decides what the sequence is.
- Classify a command from its complete protocol shape, not from its final byte alone. For example, a private CSI ending in `m` is not automatically SGR.
- Keep protocol numbers behind names that describe their standard meaning. Do not add application-name, version, prompt-text, or screenshot-specific branches to repair a parser defect.

## Terminal State And Rendering

- The terminal model owns protocol semantics. The renderer consumes typed cell and frame state and must not infer erase, link, selection, decoration, or application meaning from literal glyphs or pixels.
- Distinguish printable spaces from placeholder blanks created by erase, clear, scroll, insert, delete, or wide-cell continuation. They can render similarly while having different selection and decoration behavior.
- Represent wide characters with an explicit lead/continuation contract. Insert, overwrite, erase, resize, selection, cursor movement, and damage tracking must never leave orphan continuation cells.
- Render preedit/marked text as an overlay owned by the platform input method. Only committed text may mutate the terminal stream or screen model.
- Keep host-side frame and shader/GPU buffer layouts synchronized with an executable or structural verification gate.

## Event Semantics And Notifications

- Convert recognized control protocols into typed events at the parser boundary. Preserve producer-supplied title, subtitle, body, working directory, exit status, and other fields according to the protocol instead of scraping rendered rows.
- Treat payload-free signals as payload-free. A bell can request attention but cannot supply a task title, response body, program identity, or completion result.
- Window-title metadata, progress reports, shell command boundaries, desktop messages, and bells are distinct event families. A shared terminator or similar text does not make them interchangeable.
- Do not infer interactive task completion from output volume, a quiet timer, cursor position, or screen text. If the producer emits no completion-bearing protocol event, preserve that unknown instead of manufacturing one.
- Identify the terminal and foreground program truthfully. Do not impersonate another terminal brand or strip platform suffixes from executable names with product-specific tables; prefer explicit protocol metadata and the original invocation name when available.

## Security Boundaries

- Treat terminal-originated clipboard, file, notification, hyperlink, and shell-integration requests as untrusted external input.
- Put sensitive protocols such as clipboard read/write behind an explicit policy that considers origin, operation, payload size, and user consent. Parse and evaluate first; mutate the platform resource only after an allow decision.
- Do not log raw terminal output, pasted text, command history, environment dumps, or notification bodies by default. Diagnostic logs should prefer event names, byte counts, sequence classes, and lifecycle metadata.

## Verification

- Feed raw byte fixtures through the real parser. Cover complete sequences, every supported terminator, fragmented reads at multiple boundaries, omitted parameters, colon subparameters, private variants, invalid values, and overflow recovery.
- Add negative classification tests for lookalike protocols so one family cannot mutate another family's state.
- For rendering bugs, test the model transition and cell metadata first, then verify pixels or an installed application only where the user-visible path requires it.
- For notifications and shell integration, test field preservation and prove that ordinary output, screen repainting, title changes, progress events, and output quiescence do not synthesize desktop messages.
- When behavior depends on PTY, input-method, notification, bundle, or OS lifecycle, unit tests are necessary but not sufficient; capture event-flow evidence from the packaged application.
