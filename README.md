# code-rule

A portable engineering rulebook for projects worked on by AI coding agents.

Copy `AGENTS.md` into a project root, add the rule packs that apply, and every agent and
reviewer starts from the same defaults for architecture, naming, type safety, testing,
tokens, review, and release.

## How the rules resolve

The `AGENTS.md` closest to a file wins. Broad rules live at the project root; narrower
packs sit next to the code they govern and override the root where they disagree.

```text
my-app/
  AGENTS.md              ← the root contract, always
  src/AGENTS.md          ← narrower, overrides the root here
  ios/AGENTS.md
```

## Choosing packs

Start with the root `AGENTS.md`. Add packs by what the project is — most projects match
more than one row.

| Project | Packs to add under `rules/` |
| --- | --- |
| Any project | `git`, `config`, `constants`, `docs`, `errors`, `review`, `security-privacy`, `testing` |
| TypeScript | `typescript`, `eslint` |
| React / Next.js web | `react`, `next`, `pnpm`, `classnames`, `design-tokens`, `state-management`, `forms`, `api`, `accessibility` |
| Styling and component workshop | `tailwind`, `storybook`, `responsive-layout`, `assets` |
| React Native / Expo | `react-native`, `expo`, `android`, `ios`, `navigation`, `storage`, `accessibility`, `responsive-layout` |
| Monorepo | `monorepo`, `dependencies`, `ci`, `release` |
| Native desktop, native core, cross-language bridge | `native-desktop`, `assets`, `performance`, `release` |
| Terminal emulator, shell host, PTY frontend | `terminal-emulator`, `native-desktop`, `concurrency-async` |
| Time-based media: video, subtitles, animation, thumbnails | `media-rendering`, `assets`, `performance`, `architecture` |
| A model or agent generates, judges, or reviews the output | `ai-agent-governance`, `architecture`, `errors` |
| Runs in production | `logging-observability`, `performance` |

`ls rules/` lists every pack; each one states its own scope in its first paragraph.

## Applying them

1. Copy the root `AGENTS.md` to the project root.
2. Copy each pack you chose to the directory it governs.
3. Merge packs into one file only if the project insists on a single `AGENTS.md`.
4. When the project outgrows a rule, change the rule and the code in the same commit.

Step 4 is the one that decides whether this stays useful. A rule nobody updated is a rule
everybody learns to skip.

## What these defaults prefer

Explicit boundaries over clever coupling. Strict layers over convenient cross-layer
imports. `unknown` plus validation over `any`. Constants and tokens over inline values.
Lifecycle ownership and bounded memory over implicit long-lived state. Evidence that a
change was exercised over a green build.

They are opinionated on purpose: the point is to settle the arguments a review would
otherwise have every week, and to give an agent the same baseline a senior engineer would
enforce by hand.
