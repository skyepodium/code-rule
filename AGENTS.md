# Yulmoc - 코딩 규칙과 아키텍처 계약

시니어 엔지니어 기준의 단일 소스 규칙 문서입니다. 이 문서는 저장소 루트 아래 모든 파일에 적용됩니다.

## 우선순위

1. 현재 파일에서 가장 가까운 `AGENTS.md`
2. 루트 `AGENTS.md`
3. `docs/plan.md`
4. `DESIGN.md`
5. 일반 관행

충돌이 있으면 더 좁은 범위의 `AGENTS.md`를 따른다. 규칙을 바꿀 때는 관련 문서와 예시를 함께 갱신한다.

## 메타 규칙

- 규칙 위반을 발견하면 같은 작업 범위에서 안전하게 고칠 수 있을 때 즉시 고친다.
- 무관한 cleanup은 같은 PR에 섞지 않는다.
- AI가 수정하는 코드도 동일한 규칙을 따른다.
- 새 매직 넘버나 매직 문자열을 만들면 즉시 도메인 상수 파일로 옮긴다.
- 코드보다 규칙이 오래되었다고 판단되면 먼저 근거를 남기고 규칙을 갱신한다.

## 언어와 이름

- 주석, PR 제목, PR 본문, 이슈 제목, 이슈 본문은 한국어로 작성한다.
- 식별자, 파일명, 타입명, 함수명은 영어로 작성한다.
- 불필요한 약어를 금지한다. 예: `auth` 대신 `authentication`, `cfg` 대신 `configuration`.
- 클래스, 타입, React 컴포넌트는 `PascalCase`를 사용한다.
- 함수, 메서드, 변수, 매개변수는 `camelCase`를 사용한다.
- 전역 불변 상수는 `SCREAMING_SNAKE_CASE`를 사용하고 단위가 있으면 `_PX`, `_MS`, `_RATIO`, `_COUNT`처럼 이름에 포함한다.
- 일반 TypeScript 파일은 `camelCase.ts`, React 컴포넌트 파일은 `PascalCase.tsx`를 사용한다.

## TypeScript 기본값

- `any`는 금지한다. 외부 입력은 `unknown`으로 받고 narrowing 또는 schema 검증 후 사용한다.
- 함수 선언문은 금지한다. `const functionName = (...) => {}` 형태의 화살표 함수 표현식을 사용한다.
- import는 `~/...` 절대경로를 기본으로 한다. 같은 폴더 내부에서만 상대경로를 허용한다.
- 새 TypeScript 프로젝트는 `tsconfig`, bundler, test runner가 모두 같은 `~/...` alias를 해석하도록 설정한다.
- 중첩 조건문보다 guard clause와 early return을 우선한다. 실패, 권한 없음, 데이터 없음, 플랫폼 제외 같은 조건은 함수 앞에서 빠르게 반환한다.
- catch 값은 `unknown`으로 취급하고 `instanceof Error` 또는 별도 narrowing 후 사용한다.
- 빈 `catch`는 금지한다. 복구 전략이나 로깅 의도를 한국어 주석으로 남긴다.

## 구조와 엔트리 포인트

- 엔트리 포인트는 bootstrap과 wiring만 담당한다. 예: `main.ts`, `index.tsx`, `App.tsx`, root provider, root router, native app delegate/activity.
- 엔트리 포인트에 네트워크, storage, 알림, 결제, 인증, native bridge 같은 세부 비즈니스 로직을 직접 넣지 않는다.
- 로직이 커지면 hook, service, adapter, pure utility로 분리하고 엔트리 포인트는 의미가 드러나는 함수 호출만 조합한다.
- side effect는 service나 adapter 경계에 격리하고, UI 컴포넌트는 화면 조립과 사용자 입력 연결에 집중한다.

## Next.js 기본값

- App Router를 기본 라우팅 모델로 사용한다.
- 서버 컴포넌트를 기본값으로 두고, 브라우저 API나 상호작용이 필요한 가장 작은 컴포넌트에만 `"use client"`를 둔다.
- `page.tsx`, `layout.tsx`, `loading.tsx`, `error.tsx`, `route.ts`의 역할을 섞지 않는다.
- 라우트 핸들러도 함수 선언문 대신 `export const GET = async (...) => {}` 형태를 사용한다.

## 패키지와 도구

- 패키지 매니저는 pnpm만 사용한다.
- `package-lock.json`, `yarn.lock`, npm/yarn 명령 도입을 금지한다.
- 앱과 패키지는 가능한 `packageManager` 필드에 pnpm 버전을 명시한다.
- 의존성 추가는 `pnpm add`, 개발 의존성 추가는 `pnpm add -D`를 사용한다.
- PR 전에 기본적으로 `pnpm lint`, `pnpm typecheck`, 필요한 경우 `pnpm test`, `pnpm build`를 통과시킨다.

## UI className

- 조건부 `className` 조합은 `classnames`를 사용한다.
- 조건부 class 문자열을 `+`, template literal, 배열 `join`으로 직접 조합하지 않는다.
- 정적 class 문자열은 인라인 허용한다. 조건이 들어가면 `classNames(...)`로 바꾼다.

## 매직 넘버와 상수

- 인라인 숫자와 도메인 문자열은 원칙적으로 금지한다.
- 상수는 `src/shared/constants/<domain>.ts`에 도메인별로 둔다.
- 서로 강하게 관련된 상수가 3개 이상이면 기능 단위 객체로 묶고 `Object.freeze` 또는 `as const`로 불변 처리한다.
- 호출부는 의미가 드러나게 `VIEWPORT_TOOLTIP.OFFSET_X_PX`처럼 접근한다.

## 디자인 토큰

- 색상, spacing, radius, typography, elevation, opacity, component 치수는 디자인 토큰으로 관리한다.
- UI 컴포넌트에서 hex color, `rgba(...)`, font size, spacing, radius, opacity 같은 시각 값을 직접 선언하지 않는다.
- 토큰은 `src/shared/design/tokens.ts` 또는 플랫폼별 design token 경계에 둔다.
- 제품/도메인 상수와 디자인 토큰을 섞지 않는다. 예: polling interval은 constants, button radius는 design token이다.

## PR 규칙

- PR 대상 브랜치는 `develop`이다.
- PR 본문에는 `## 참여자 (participant)` 섹션을 포함하고 참여한 AI 에이전트를 명시한다.
- PR은 구현 의도, 검증 결과, 남은 위험을 한국어로 적는다.
