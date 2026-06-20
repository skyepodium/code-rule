# Monorepo 규칙

이 디렉토리는 workspace, package boundary, internal import 규칙을 정의한다.

## workspace

- workspace 범위는 `pnpm-workspace.yaml`에 명시한다.
- package 이름, ownership, publish/private 여부를 명확히 한다.
- 루트 dependency와 package dependency를 구분한다.

## package boundary

- 다른 package의 내부 파일을 deep import하지 않는다.
- public entry point를 통해 import한다.
- shared package는 앱 세부 구현을 import하지 않는다.
- 순환 dependency가 생기면 공통 타입/utility를 더 낮은 package로 분리한다.

## scripts

- root script는 workspace 전체 계약을 담당한다.
- package script는 해당 package 안에서 독립 실행 가능해야 한다.
- generated output 위치와 커밋 여부를 package별로 명시한다.
