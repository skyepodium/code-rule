# 테스트 규칙

이 디렉토리는 unit, integration, component 테스트 규칙을 정의한다.

## 기본 원칙

- 변경된 동작에는 테스트를 먼저 추가하거나 기존 테스트를 갱신한다.
- 버그 수정은 실패하는 회귀 테스트로 증상을 고정한 뒤 고친다.
- 테스트 이름은 기대 동작을 설명한다. `works`, `test1`처럼 의미 없는 이름을 쓰지 않는다.
- 테스트는 구현 세부보다 public interface와 사용자 관찰 가능 동작을 검증한다.

## 파일과 fixture

- 테스트 파일은 대상 파일 옆의 `*.test.ts(x)` 또는 가까운 `__tests__/`에 둔다.
- fixture 값도 매직 값이면 테스트 파일 안의 named constant로 둔다.
- 대형 fixture는 builder 또는 fixture factory로 분리한다.
- snapshot은 구조가 안정적이고 리뷰 가능한 경우에만 사용한다.

## mock

- mock은 외부 시스템, 시간, 랜덤, native bridge, 네트워크처럼 통제 불가능한 경계에만 사용한다.
- 같은 프로세스의 순수 함수나 도메인 로직은 mock하지 않는다.
- timer, interval, listener, subscription은 테스트 종료 시 cleanup한다.
- 비동기 테스트는 pending promise와 open handle을 남기지 않는다.

## 검증

- PR 전 `pnpm test`를 통과시킨다.
- 테스트가 너무 느리면 느린 원인을 분리하고 unit 테스트와 integration 테스트를 나눈다.
