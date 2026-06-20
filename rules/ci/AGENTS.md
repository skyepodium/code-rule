# CI 규칙

이 디렉토리는 CI job, cache, 검증 순서 규칙을 정의한다.

## 기본 job

- CI는 lockfile 기반 설치를 사용한다.
- 기본 검증 순서는 install, lint, typecheck, test, build다.
- 실패한 job을 우회하지 않고 원인을 수정한다.

## pnpm

- pnpm store cache를 사용하되 lockfile 변경 시 정확히 invalidation되게 한다.
- CI 명령 예시는 pnpm만 사용한다.
- workspace는 변경 범위 기반 job을 쓰더라도 root-level 계약을 깨지 않는다.

## artifact

- build artifact, coverage, test report는 필요한 job에서만 저장한다.
- secret이 artifact에 포함되지 않게 한다.
