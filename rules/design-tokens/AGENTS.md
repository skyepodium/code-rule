# 디자인 토큰 규칙

이 디렉토리는 UI 시각 값과 디자인 시스템 토큰 경계를 정의한다. 대상 프로젝트에서는 `src/`, `app/`, `features/`, `components/`처럼 UI 코드가 있는 가장 가까운 디렉토리에 둔다.

## 기본 규칙

- 색상, spacing, radius, typography, elevation, opacity, z-index, component 치수는 디자인 토큰으로 관리한다.
- UI 컴포넌트에서 hex color, `rgba(...)`, font size, spacing, radius, opacity 값을 직접 선언하지 않는다.
- 토큰은 `src/shared/design/tokens.ts` 또는 플랫폼별 design token 경계에 둔다.
- 토큰 파일은 제품 UI 언어를 표현하고, API path, storage key, timeout 같은 도메인 상수와 섞지 않는다.

## 토큰 분류

- 색상은 `COLOR_TOKENS`처럼 역할 기반 이름을 사용한다. 예: `SURFACE_PANEL`, `CONTENT_PRIMARY`, `ACCENT_PRIMARY`.
- spacing은 `SPACE_TOKENS`로 관리하고 화면 padding, gap, compact spacing을 의미 이름으로 둔다.
- radius는 `RADIUS_TOKENS`로 관리한다.
- typography는 `TYPOGRAPHY_TOKENS`로 관리하고 단위가 있는 이름을 사용한다.
- 특정 컴포넌트의 고정 치수는 `COMPONENT_TOKENS`로 관리한다.

## 호출부 규칙

- 컴포넌트는 토큰을 import해 사용한다.
- 컴포넌트 내부에서 토큰 값을 다시 alias하거나 의미를 흐리는 이름으로 재정의하지 않는다.
- 동일 숫자라도 의미가 다르면 다른 토큰으로 둔다. 예: 화면 gap과 버튼 padding이 모두 `16`이어도 같은 토큰으로 묶지 않는다.
- 임시 시각 값을 추가할 때도 먼저 토큰을 만든 뒤 사용한다.

## 플랫폼별 UI

- React Native, Android native, iOS native처럼 플랫폼별 UI가 있으면 각 플랫폼에 대응하는 token 경계를 둔다.
- native UI에도 색상과 치수를 직접 쓰지 않는다. 플랫폼 언어의 token object 또는 resource를 통해 사용한다.
- cross-platform 토큰과 native 전용 토큰이 갈라질 때는 이름과 역할이 대응되게 유지한다.

## 금지 패턴

- `style={{ color: '#ffffff' }}`처럼 컴포넌트에 색상을 직접 쓰지 않는다.
- `fontSize: 16`, `borderRadius: 8`, `opacity: 0.72`처럼 시각 값을 style에 직접 쓰지 않는다.
- `constants.ts`에 디자인 토큰과 비즈니스 상수를 함께 넣지 않는다.
