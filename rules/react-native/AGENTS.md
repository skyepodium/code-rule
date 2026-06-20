# React Native 규칙

이 디렉토리는 React Native 앱, platform 분기, native bridge 규칙을 정의한다.

## 구조

- `App.tsx`, `index.js`, native app delegate/activity는 bootstrap과 wiring만 담당한다.
- native bridge 직접 접근은 adapter에 격리한다.
- 권한, AppState, Linking, DeviceEventEmitter, NativeModules 같은 platform side effect는 service 또는 adapter 경계에서 감싼다.
- 플랫폼 분기는 가능한 `*.ios.ts`, `*.android.ts` 또는 platform adapter에 모은다.

## UI

- 시각 값은 디자인 토큰을 사용한다.
- `StyleSheet.create`를 기본으로 사용하고 inline style은 동적 값이 필요한 좁은 범위에만 둔다.
- touch target, safe area, keyboard avoidance, text overflow를 기본 검토한다.
- list는 데이터 규모가 커질 수 있으면 virtualization을 전제로 설계한다.

## native 연동

- native module 이름, event name, permission key는 상수화한다.
- native listener 등록은 중복 등록 방지와 cleanup API를 가진다.
- bridge로 주고받는 payload는 TypeScript 타입과 native parsing 경계를 함께 관리한다.
- Android/iOS native 구현은 JS 서비스 계약을 깨지 않게 adapter 뒤에 숨긴다.
