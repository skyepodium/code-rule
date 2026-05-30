# 상수와 매직 값 규칙

이 디렉토리는 매직 넘버와 매직 문자열을 금지하고 도메인 상수로 관리하는 규칙을 정의한다. 대상 프로젝트에서는 `src/shared/constants/` 또는 상수 디렉토리에 둔다.

## 기본 규칙

- 모든 매직 넘버와 도메인 매직 문자열은 상수로 분리한다.
- 상수 파일은 `src/shared/constants/<domain>.ts`에 둔다.
- 도메인별로 파일을 나눈다. 예: `viewport.ts`, `pagination.ts`, `route.ts`, `animation.ts`.
- `constants.ts` 하나에 모든 값을 몰아넣지 않는다.
- timeout, interval, animation duration, spring config, gesture threshold, hit slop, retry count, page size, cache TTL, vibration pattern, storage key, route path, event name, query key, permission key, header key는 호출부에 직접 쓰지 않는다.

## 이름 규칙

- 전역 상수는 `SCREAMING_SNAKE_CASE`를 사용한다.
- 단위가 있으면 이름에 포함한다.
- 픽셀은 `_PX`, 밀리초는 `_MS`, 비율은 `_RATIO`, 개수는 `_COUNT`, 길이는 `_LENGTH`를 사용한다.
- 초 단위 값은 `_SECONDS`, 분 단위 값은 `_MINUTES`, 바이트 단위 값은 `_BYTES`를 사용한다.
- boolean 의미를 갖는 값은 긍정형 이름을 사용한다.

## 객체 상수

- 서로 강하게 관련된 상수가 3개 이상이면 기능 단위 객체로 묶는다.
- 객체명은 도메인과 역할을 드러낸다.
- 내부 key도 `SCREAMING_SNAKE_CASE`와 단위를 유지한다.
- 객체는 `Object.freeze` 또는 `as const`로 불변 처리한다.

```ts
const VIEWPORT_TOOLTIP = Object.freeze({
  OFFSET_X_PX: 12,
  OFFSET_Y_PX: -28,
  FONT_SIZE_PX: 12,
});

export { VIEWPORT_TOOLTIP };
```

## 호출부 규칙

- 호출부는 `VIEWPORT_TOOLTIP.OFFSET_X_PX`처럼 의미가 드러나게 접근한다.
- 상수를 import할 때 alias로 의미를 흐리지 않는다.
- 단 한 곳에서만 쓰여도 의도가 중요하면 상수화한다.
- 테스트 fixture의 값은 테스트 파일 안의 named constant로 둔다.

## 허용 가능한 인라인 값

- 언어 관용에 가까운 `0`, `1`, `-1`은 lint 설정에서 제한적으로 허용할 수 있다.
- 빈 문자열, boolean literal, `null`, `undefined`는 매직 값 규칙 대신 타입과 도메인 의미로 판단한다.
- CSS class token은 `classnames` 규칙을 따른다.
- HTTP method, route path, storage key, event name, query key는 도메인 문자열이므로 상수화한다.

## 금지 패턴

- `setTimeout(callback, 300)`처럼 시간 값을 인라인으로 두지 않는다.
- `style={{ width: 320 }}`처럼 크기 값을 인라인으로 두지 않는다.
- `"user-id"` 같은 storage key나 header key를 호출부에 직접 쓰지 않는다.
- 같은 숫자를 여러 곳에 복사하지 않는다. 같은 숫자가 우연히 같아도 의미가 다르면 다른 상수로 둔다.
