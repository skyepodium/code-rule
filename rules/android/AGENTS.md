# Android 규칙

이 디렉토리는 Android native 코드와 설정 규칙을 정의한다.

## Manifest와 권한

- permission 추가 시 사용 목적과 사용자 안내 흐름을 함께 구현한다.
- activity, service, receiver의 `exported` 값을 명시한다.
- foreground service는 notification channel과 stop 경로를 가진다.
- special permission은 설정 화면 이동 후 상태 재확인 흐름을 둔다.

## Kotlin/Java

- Android entry point는 wiring만 담당한다.
- business logic은 service, manager, adapter로 분리한다.
- native token/resource를 사용하고 색상/치수를 view에 직접 쓰지 않는다.
- listener, callback, handler, runnable은 lifecycle에서 해제한다.

## Resource

- resource 이름은 소문자 snake_case를 사용한다.
- 문자열은 가능한 resource로 분리하되 bridge contract key는 상수로 둔다.
- density별 asset과 adaptive icon 요구사항을 확인한다.
