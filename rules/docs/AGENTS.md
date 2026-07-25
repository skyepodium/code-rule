# Documentation Rules

This directory defines README, ADR, runbook, and development documentation rules.

## README

- README files must include installation, execution, verification, environment variables, and the main structure.
- Command examples must follow the project's package manager.
- Do not leave stale template text or unused commands.

## Design Documents

- Record important architecture decisions with intent, alternatives, decision, and impact.
- Specify temporary constraints and removal conditions.
- If documentation diverges from code, update it in the same change.

## Operations Documents

- Deployment, rollback, migration, and incident response procedures must include executable commands and verification methods.
- Do not write sensitive secret values directly in documentation.

## Diagrams

- Do not draw one diagram of everything. Separate the rule from its exceptions: one diagram shows the intended shape, another shows every edge that deviates from it.
- Make the exception diagram exhaustive by contract and say so, so that an edge absent from it is known to follow the rule and must not be re-drawn per module.
- Keep node labels short enough to read at a glance. A diagram nobody can parse is worse than a list.
- Validate diagram source in the same change that edits it. A diagram that fails to render is an outage of the document.

## Translated Documents

- Name one language canonical and keep translations as sibling files with a language suffix, cross-linked at the top of each.
- Refresh the translation in the same change that edits the canonical document, or add an explicit stale marker at the top of the translation.
- Keep code blocks, diagram source, commands, and identifiers byte-identical across the pair. Translate prose only, and verify the equality mechanically when the pair matters.

## Documents as Contracts

- A document that states a behavior the code does not implement is a defect, not a plan. Either implement it or mark it as unimplemented in the document.
- When a document declares a threshold, sequence, or ban, the enforcing code is the authority and the document must cite where it lives.
- Record the reason a rule exists next to the rule. A rule with no recorded reason gets removed by the next person who finds it inconvenient.

