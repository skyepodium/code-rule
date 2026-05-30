# 아키텍처와 책임 경계 규칙

이 디렉토리는 프로젝트 구조, 엔트리 포인트, side effect 경계, 파일 책임을 정의한다. 대상 프로젝트에서는 앱 루트, `src/`, `app/`, `features/`처럼 실행 흐름을 조립하는 가장 가까운 디렉토리에 둔다.

## 엔트리 포인트

- 엔트리 포인트는 최대한 얇게 유지한다.
- `main.ts`, `index.tsx`, `App.tsx`, root provider, root router, native app delegate/activity, server entry는 bootstrap과 wiring만 담당한다.
- 엔트리 포인트에서 직접 비즈니스 규칙을 계산하지 않는다.
- 네트워크, storage, 알림, 인증, 결제, native bridge, analytics 같은 세부 구현은 service나 adapter로 분리한다.
- 엔트리 포인트는 초기화 순서, provider 연결, router 연결, 전역 listener 등록, 최상위 에러 경계 연결만 조합한다.

## 책임 경계

- UI 컴포넌트는 화면 조립, 표시 상태, 사용자 입력 연결에 집중한다.
- hook은 UI 생명주기와 도메인/service 호출을 연결한다.
- service는 side effect와 외부 시스템 접근을 담당한다.
- utility는 side effect 없는 순수 계산만 담당한다.
- adapter는 프레임워크, 플랫폼, SDK, native bridge 같은 외부 경계를 감싼다.
- 모델과 타입은 도메인 의미를 표현하고 UI 또는 SDK 세부 타입을 불필요하게 끌어오지 않는다.

## 의존성 방향

- 상위 레이어가 하위 레이어를 호출한다. 하위 레이어가 화면, router, framework entry를 import하지 않는다.
- 순환 의존성이 생기면 공통 타입, 순수 유틸, adapter 인터페이스를 더 낮은 레이어로 분리한다.
- SDK 객체를 앱 전체에 직접 퍼뜨리지 않는다. 필요한 기능만 service/adapter 함수로 감싼다.
- platform/framework 조건은 가능한 경계 모듈에 모은다. 호출부는 의미 있는 함수 이름으로 사용한다.

## 파일 크기와 분리 기준

- 한 파일은 한 가지 역할만 가진다.
- 600 LOC를 넘으면 분리 후보로 본다.
- 상태, gesture, playback, navigation, permission, storage처럼 서로 다른 변화 이유가 한 파일에 섞이면 분리한다.
- 분리는 동작 변경 없이 작은 단위로 한다. 먼저 테스트나 기존 동작 확인으로 회귀 기준을 잡는다.

## 전역 상태

- 전역 mutable singleton은 새로 만들지 않는다.
- 프로세스 단위 상태가 필요하면 service 경계에 가두고 lifecycle, reset, cleanup API를 명시한다.
- 테스트에서 초기화할 수 없는 전역 상태는 설계 냄새로 본다.
- 캐시, 큐, listener registry는 만료/해제/중복 등록 방지 규칙을 코드로 드러낸다.

## 제어 흐름

- guard clause와 early return을 우선해 happy path를 얕게 유지한다.
- 실패, 권한 없음, 데이터 없음, 플랫폼 제외, disabled/no-op 조건은 함수 앞쪽에서 반환한다.
- 여러 조건을 하나의 긴 boolean으로 숨기지 않는다. 도메인 의미가 있는 조건은 helper로 이름을 붙인다.
