# code-rule

개인 코딩 규칙을 `AGENTS.md` 단위로 나눈 저장소입니다.

## 구성

- `AGENTS.md`: 모든 프로젝트에 적용할 공통 계약
- `rules/typescript/AGENTS.md`: TypeScript 타입 안정성, 함수 표현식, import 규칙
- `rules/testing/AGENTS.md`: 테스트 작성, mock, fixture, 회귀 테스트 규칙
- `rules/react/AGENTS.md`: React 컴포넌트, hook, effect, props 규칙
- `rules/react-native/AGENTS.md`: React Native와 native bridge, platform 경계 규칙
- `rules/next/AGENTS.md`: Next.js App Router, 서버/클라이언트 컴포넌트, 라우트 핸들러 규칙
- `rules/pnpm/AGENTS.md`: pnpm 사용, lockfile, workspace, script 규칙
- `rules/classnames/AGENTS.md`: `classnames` 기반 className 조합 규칙
- `rules/eslint/AGENTS.md`: ESLint 필수 규칙과 검사 범위
- `rules/constants/AGENTS.md`: 매직 넘버와 매직 문자열 상수화 규칙
- `rules/design-tokens/AGENTS.md`: 색상, spacing, typography 같은 UI 토큰 규칙
- `rules/architecture/AGENTS.md`: 엔트리 포인트, 책임 경계, side effect 격리 규칙
- `rules/errors/AGENTS.md`: 에러 모델, 로깅, 사용자 메시지 분리 규칙
- `rules/storage/AGENTS.md`: storage key, schema, migration, 민감 정보 저장 규칙
- `rules/api/AGENTS.md`: API adapter, schema 검증, timeout/retry 규칙
- `rules/state-management/AGENTS.md`: local/server/global state 경계 규칙
- `rules/security-privacy/AGENTS.md`: secret, PII, 권한, 외부 SDK 보안 규칙
- `rules/accessibility/AGENTS.md`: 접근성 label, touch target, focus, contrast 규칙
- `rules/responsive-layout/AGENTS.md`: 반응형 layout, safe area, overflow 규칙
- `rules/assets/AGENTS.md`: 이미지, 아이콘, 폰트, asset naming 규칙
- `rules/forms/AGENTS.md`: form state, validation, submit, error 표시 규칙
- `rules/navigation/AGENTS.md`: route 상수, params 타입, deep link 규칙
- `rules/git/AGENTS.md`: branch, commit, generated file, history 규칙
- `rules/review/AGENTS.md`: self-review, PR checklist, reviewer 응답 규칙
- `rules/dependencies/AGENTS.md`: dependency 도입, license, bundle, 보안 기준
- `rules/config/AGENTS.md`: 환경 변수, runtime/build config, feature flag 규칙
- `rules/logging-observability/AGENTS.md`: logger, analytics, crash reporting 규칙
- `rules/performance/AGENTS.md`: render, list, bundle, bridge 성능 규칙
- `rules/concurrency-async/AGENTS.md`: abort, race, timer/listener cleanup 규칙
- `rules/android/AGENTS.md`: Android manifest, permission, service, resource 규칙
- `rules/ios/AGENTS.md`: iOS plist, entitlement, Swift bridge, background mode 규칙
- `rules/expo/AGENTS.md`: Expo managed/prebuild/EAS/config plugin 규칙
- `rules/tailwind/AGENTS.md`: Tailwind token, arbitrary value, class 조합 규칙
- `rules/storybook/AGENTS.md`: story 상태, 문서화, visual regression 규칙
- `rules/docs/AGENTS.md`: README, ADR, runbook, 문서 명령 규칙
- `rules/release/AGENTS.md`: versioning, changelog, artifact, rollout 규칙
- `rules/ci/AGENTS.md`: CI job, pnpm cache, 검증 순서 규칙
- `rules/monorepo/AGENTS.md`: workspace, package boundary, internal import 규칙

## 사용 방식

대상 프로젝트의 성격에 맞게 필요한 `AGENTS.md`를 복사하거나 병합합니다. 루트 공통 규칙을 먼저 두고, 더 좁은 디렉토리에 세부 규칙을 배치하면 가까운 `AGENTS.md`가 우선합니다.
