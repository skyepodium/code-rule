# TypeScript 규칙

이 디렉토리는 TypeScript와 React TypeScript 코드 규칙을 정의한다. 대상 프로젝트에 복사할 때는 `src/`, `app/`, `lib/`, `components/`처럼 TypeScript 코드가 있는 가장 가까운 디렉토리에 둔다.

## 타입 안전성

- `any`는 금지한다. 필요한 경우 `unknown`으로 받고 좁힌다.
- 외부 입력은 schema 검증 또는 명시적 narrowing을 거쳐 도메인 타입으로 변환한다.
- public export 함수와 React 컴포넌트 props는 타입을 명시한다.
- `as` 단언은 마지막 수단이다. 사용 시 왜 안전한지 코드 구조로 드러나야 한다.
- non-null assertion인 `!`는 금지한다. 분기, guard, early return으로 좁힌다.

## 함수 표현식

- 함수 선언문은 금지한다.
- 일반 함수는 `const functionName = (...) => {}` 형태의 화살표 함수 표현식을 사용한다.
- React 컴포넌트도 `const ComponentName = (props: Props) => {}` 형태로 작성하고 export는 아래에 둔다.
- hook은 `const useThing = (...) => {}` 형태로 작성한다.
- overload가 꼭 필요하면 타입 alias와 구현 함수를 분리한다.

## 제어 흐름

- guard clause와 early return을 적극 사용한다.
- 실패, 권한 없음, 데이터 없음, 플랫폼 제외, disabled/no-op 조건은 함수 앞쪽에서 빠르게 반환한다.
- `return`, `throw`, `continue`, `break` 이후의 `else`는 피하고 happy path가 덜 들여쓰기되게 작성한다.
- early return 조건이 도메인 지식을 담고 있으면 boolean helper나 named constant로 의미를 드러낸다.
- 여러 조건을 한 줄에 숨기지 않는다. 독립적인 실패 조건은 읽히는 순서대로 나눈다.

## import와 모듈

- import는 `~/...` 절대경로를 기본으로 한다.
- 같은 폴더 내부 파일만 `./file` 상대경로를 허용한다.
- 타입 전용 import는 `import type`을 사용한다.
- 순환 의존성을 만들지 않는다. 발생하면 공통 타입이나 순수 유틸을 더 낮은 레이어로 분리한다.
- 모듈 top-level 가변 싱글톤을 금지한다. 서비스는 인자, props, context, factory로 주입한다.

## 에러 처리

- `try/catch`에서 잡은 값은 `unknown`으로 취급한다.
- `instanceof Error` 또는 명시적 guard 후 메시지와 원인을 사용한다.
- 빈 `catch`는 금지한다. 복구하거나 로깅하거나 다시 던진다.
- UI에 노출되는 에러 메시지는 도메인별 상수 또는 메시지 맵으로 관리한다.

## 파일 경계

- 한 파일은 한 가지 역할만 가진다.
- 600 LOC를 넘으면 분할을 검토한다.
- React 컴포넌트 파일에는 컴포넌트, props 타입, 작은 렌더 보조 함수까지만 둔다.
- 비즈니스 로직은 순수 함수로 빼고 side effect는 service나 adapter 모듈에 격리한다.
