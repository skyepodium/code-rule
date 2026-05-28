# code-rule

개인 코딩 규칙을 `AGENTS.md` 단위로 나눈 저장소입니다.

## 구성

- `AGENTS.md`: 모든 프로젝트에 적용할 공통 계약
- `rules/typescript/AGENTS.md`: TypeScript 타입 안정성, 함수 표현식, import 규칙
- `rules/next/AGENTS.md`: Next.js App Router, 서버/클라이언트 컴포넌트, 라우트 핸들러 규칙
- `rules/pnpm/AGENTS.md`: pnpm 사용, lockfile, workspace, script 규칙
- `rules/classnames/AGENTS.md`: `classnames` 기반 className 조합 규칙
- `rules/eslint/AGENTS.md`: ESLint 필수 규칙과 검사 범위
- `rules/constants/AGENTS.md`: 매직 넘버와 매직 문자열 상수화 규칙

## 사용 방식

대상 프로젝트의 성격에 맞게 필요한 `AGENTS.md`를 복사하거나 병합합니다. 루트 공통 규칙을 먼저 두고, 더 좁은 디렉토리에 세부 규칙을 배치하면 가까운 `AGENTS.md`가 우선합니다.

