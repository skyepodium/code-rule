# Navigation 규칙

이 디렉토리는 route, navigation params, deep link 규칙을 정의한다.

## route

- route path/name은 상수화한다.
- route params 타입을 명시한다.
- 화면 컴포넌트는 params parsing을 adapter/helper로 분리한다.
- optional param은 fallback과 invalid state를 처리한다.

## 이동

- 내부 이동은 프로젝트 표준 navigation API를 사용한다.
- push/replace/back/reset의 의미를 구분한다.
- auth guard, permission guard, onboarding guard는 한 경계에 모은다.

## deep link

- deep link schema와 route mapping을 문서화한다.
- 알 수 없는 deep link는 안전한 fallback으로 보낸다.
- 외부 URL open 전 allowlist 또는 scheme 검증을 한다.
