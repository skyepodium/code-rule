# Dependency 규칙

이 디렉토리는 패키지와 SDK 도입 기준을 정의한다.

## 도입 기준

- 기존 유틸이나 플랫폼 API로 해결할 수 있으면 새 dependency를 추가하지 않는다.
- dependency 추가 전 maintenance, license, bundle size, native requirement, security 이슈를 확인한다.
- 런타임 import는 `dependencies`, 빌드/테스트/타입 전용은 `devDependencies`에 둔다.
- workspace 내부 패키지는 가능한 `workspace:*`를 사용한다.

## 변경

- major upgrade는 breaking change와 migration guide를 확인한다.
- lockfile은 pnpm 명령으로 갱신하고 수동 편집하지 않는다.
- native dependency 추가 시 iOS/Android build 영향과 설치 단계를 문서화한다.

## 제거

- unused dependency는 import 검색과 script 사용 여부를 확인한 뒤 제거한다.
- dependency 제거 후 lint, typecheck, test, build를 실행한다.
