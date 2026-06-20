# 상태 관리 규칙

이 디렉토리는 local, server, global state 경계를 정의한다.

## 상태 분류

- local view state, form state, server state, global app state를 구분한다.
- 서버에서 다시 가져올 수 있는 데이터는 global store에 복제하지 않는다.
- props나 다른 state에서 계산 가능한 값은 derived state로 계산한다.
- URL/route가 소유해야 할 상태를 컴포넌트 내부에 숨기지 않는다.

## store

- store는 작은 slice로 나누고 public action을 통해서만 변경한다.
- selector를 사용해 불필요한 re-render를 줄인다.
- store에 SDK 객체, navigation 객체, React component를 저장하지 않는다.
- reset/cleanup API를 명시해 테스트와 logout 흐름에서 초기화할 수 있게 한다.

## side effect

- side effect는 store 내부에 숨기지 말고 service/action 경계로 분리한다.
- optimistic update는 rollback 조건과 실패 메시지를 함께 설계한다.
