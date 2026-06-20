# React 규칙

이 디렉토리는 React 컴포넌트, hook, effect 규칙을 정의한다.

## 컴포넌트

- 컴포넌트는 화면 조립, 표시 상태, 사용자 입력 연결에 집중한다.
- React 컴포넌트는 `const ComponentName = (props: Props) => {}` 형태로 작성하고 export는 아래에 둔다.
- props 타입은 명시하고 boolean props는 긍정형 이름을 사용한다.
- 컴포넌트 안에 비즈니스 규칙, API 호출 세부 구현, storage 접근을 직접 넣지 않는다.
- 반복되는 UI 상태는 작은 컴포넌트로 분리하되 props가 과도해지면 hook 또는 view model을 검토한다.

## hook과 effect

- hook은 UI lifecycle과 service 호출을 연결한다.
- `useEffect`는 외부 시스템 동기화에만 사용한다. 렌더 중 계산 가능한 derived state에는 쓰지 않는다.
- effect는 cleanup을 명시한다. timer, subscription, listener, request는 해제하거나 취소한다.
- dependency array를 숨기기 위해 lint를 끄지 않는다.
- 상태 update가 이전 상태에 의존하면 functional update를 사용한다.

## 상태

- 서버 데이터, form state, view state, global state를 섞지 않는다.
- props에서 계산 가능한 값은 별도 state로 복제하지 않는다.
- loading, disabled, error 상태는 사용자 동작과 접근성 상태에 반영한다.
