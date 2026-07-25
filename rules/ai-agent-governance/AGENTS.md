# AI Agent and Generative Pipeline Governance Rules

This directory defines rules for systems where a model (LLM, image model, or agent) produces or judges part of the output. In target projects, place it in the closest directory that owns generation, orchestration, or agent workflows, such as `agents/`, `pipeline/`, `workflows/`, or the service that calls the model.

These rules exist because generative steps are non-deterministic and persuasive. Left ungoverned, they silently narrow scope, approve their own work, and report success without evidence.

## Determinism Boundary

- Put the model inside a closed loop, not in charge of it. The model chooses and judges; deterministic code owns state transitions, retries, ordering, persistence, hashing, and verification.
- Never move a gate decision from code into a prompt. If the pipeline must decide whether to proceed, that decision belongs in code reading recorded state.
- Model output is an input to a decision, never the decision itself. Parse it, validate it against a schema, and reject it on failure.
- Keep every generated artifact reproducible from recorded inputs, or record enough evidence to audit it. Prefer deterministic renderers over model calls whenever the artifact is mechanical.
- Do not use wall-clock time or randomness in generated output except in explicitly stamped metadata fields.

## Gates and Evidence

- An artifact's existence is not an approval. Gate truth lives in an approval record bound to a content hash of the evidence, produced by the declared review sequence.
- Bind approvals to evidence hashes, not filenames. Changing the evidence must invalidate the approval automatically.
- Recompute evidence on read. A stored score, checklist, or reviewer note must never be accepted as proof of a property the code can measure itself.
- Missing evidence is a gap, not a pass. A success report must name the evidence that supports it.
- Fail closed. Ownership conflicts, evidence drift, stale derived artifacts, and audit failures stop the pipeline; they are never downgraded to warnings.
- A stale derived artifact is worse than a missing one. Block on staleness rather than shipping an out-of-date reference.

## Independent Verification

- The generator may not pass itself. Verification belongs to a different role, pass, or process than the one that produced the work.
- Emit review records with the verdict field empty and the measurable expectations pre-filled. An unfilled record surfaces as an open gap, never as a silent pass.
- Ship the review scope with the evidence. State in the record what the reviewer may judge from this artifact and what it may not be used to judge, so the boundary does not depend on the reviewer having read a document.
- When a claim is checkable by code, check it in code and let the human judge only what code cannot.

## Reference and Input Authority

- Every input supplied to a generative call declares what it is authoritative for. Two inputs must never claim the same authority without a stated precedence.
- Rank inputs explicitly, and make the payload order match the ranking. A supporting reference goes last; a primary contract goes first.
- Authority text is a constant, not per-call prose. Compose it once so no call site can quietly widen or weaken it.
- Make a single-purpose reference visibly unusable for anything else. If an artifact should convey only layout, strip it of style, texture, and finish so there is nothing else to copy. Deliberate crudeness is a feature.
- Keep a reference out of collections it does not belong to. An input that is not a style authority must not appear in the style-authority list.
- Widening what an input is authoritative for is a contract change with tests, not a prompt tweak.

## Switches and Ownership

- Every behavior switch has exactly one owner. Records that supply data must not also decide whether that data binds.
- Scope an opt-out to what it actually means. Document the cases it covers and the neighbouring cases it does not, or it will be used as a general escape hatch.
- Default the switch so the safe path needs no action.

## History and Mid-Flight Change

- History is append-only. Record rejected attempts, retries, steering, and reasons; never rewrite them.
- Chain audit entries by hash so a deleted or edited entry is detectable.
- Write audit appends durably (flush and fsync, or write-and-replace). A torn append to a hash-chained log is unrecoverable.
- Allow mid-flight plan changes only through a declared whitelist of mutations, each requiring a reason. Goals, constraints, and gate thresholds are not steerable.

## Ambiguity and Vague Requests

- Over-threshold ambiguity redirects to clarification, not to generation. Score the request against declared dimensions and set the threshold in code.
- Require non-goals and decision boundaries regardless of score. A brief without them is not ready.
- Do not ask the user what the codebase already answers. Tag facts by source and only ask about what is genuinely unknown.
- A request with no concrete anchors (no path, identifier, error, or ticket) routes to planning rather than execution.

## Role Prompts and Delegation

- Substantial agent prompts follow a fixed skeleton: identity and goal, hard constraints (file ownership, frozen interfaces, read-only or not), execution steps, output contract naming the exact required sections, and stop rules.
- One agent owns one file set. Overlapping ownership is a launch error, not a merge problem to sort out later.
- The orchestrator delegates, integrates, and judges. It does not redo a delegated task itself and never states a pending agent's result.
- Give read-only work read-only tools. Repository search, classification, transcription, and reference gathering need no write access, and removing it removes a class of accident.
- Match model tier to task shape. Use the cheapest capable tier for lookup and classification; reserve the strongest for synthesis, gate judgment, and code mutation.
- Workers escalate blockers, shared-file conflicts, and scope expansion upward instead of absorbing them.

## Reporting

- Report outcomes with evidence: the command run and its observed result, or the recorded artifact and its hash.
- State what was skipped and why. Silent narrowing of scope is the most common failure of generative pipelines.
- Do not treat a plausible summary as verification. If the check did not run, say it did not run.
