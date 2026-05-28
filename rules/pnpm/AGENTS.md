# pnpm 규칙

이 디렉토리는 pnpm 기반 패키지 관리 규칙을 정의한다. 대상 프로젝트에서는 루트 또는 workspace 루트에 둔다.

## 패키지 매니저

- 패키지 매니저는 pnpm만 사용한다.
- `npm install`, `npm run`, `npx`, `yarn`, `bun install`을 금지한다.
- `package-lock.json`, `yarn.lock`, `bun.lockb`를 만들지 않는다.
- `pnpm-lock.yaml`은 커밋 대상이다.

## 명령

- 의존성 추가는 `pnpm add <package>`를 사용한다.
- 개발 의존성 추가는 `pnpm add -D <package>`를 사용한다.
- 일회성 실행은 `pnpm exec <command>` 또는 `pnpm dlx <package>`를 사용한다.
- CI 설치는 lockfile을 고정하는 명령을 사용한다.

## script 계약

- 기본 script 이름은 `lint`, `typecheck`, `test`, `build`, `format`을 사용한다.
- Next 앱은 최소한 `pnpm lint`, `pnpm typecheck`, `pnpm build`가 동작해야 한다.
- script 안에서 OS별 shell 기능에 의존하지 않는다.
- script가 길어지면 별도 TypeScript 또는 JavaScript 스크립트 파일로 분리한다.

## workspace

- monorepo는 `pnpm-workspace.yaml`로 workspace 범위를 명시한다.
- workspace 내부 패키지 참조는 가능한 `workspace:*` 프로토콜을 사용한다.
- 루트에 의존성을 추가할 때는 실제로 루트에서 필요한지 먼저 확인한다.
- 앱 전용 의존성은 해당 앱 package에 둔다.

## 의존성 기준

- 런타임 코드에서 import되는 패키지는 `dependencies`에 둔다.
- 빌드, 테스트, 타입, 린트 전용 패키지는 `devDependencies`에 둔다.
- 새 의존성은 기존 유틸로 해결할 수 없는 경우에만 추가한다.
- 버전 충돌 해결은 lockfile 수동 편집 대신 pnpm 명령으로 처리한다.

