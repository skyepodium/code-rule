# Concurrency와 Async 규칙

이 디렉토리는 비동기 작업, cancellation, race condition 규칙을 정의한다.

## cancellation

- fetch, subscription, timer, background task는 취소 또는 cleanup 경로를 가진다.
- 컴포넌트 unmount 후 state update가 발생하지 않게 한다.
- AbortController 또는 프로젝트 표준 cancellation API를 사용한다.

## race condition

- 최신 요청만 반영해야 하는 화면은 request id, abort, stale guard를 둔다.
- 동시 submit, 중복 tap, 빠른 route 전환을 고려한다.
- optimistic update는 실패 rollback과 충돌 기준을 가진다.

## timer와 scheduler

- interval, timeout, animation frame은 cleanup한다.
- 시간 값은 상수화한다.
- background/foreground 전환 시 재개와 정지 기준을 명시한다.
