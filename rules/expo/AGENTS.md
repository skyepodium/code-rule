# Expo 규칙

이 디렉토리는 Expo managed, prebuild, EAS 규칙을 정의한다.

## 프로젝트 모드

- managed workflow와 bare/prebuild 요구사항을 먼저 구분한다.
- native custom code가 필요하면 config plugin 또는 prebuild 전략을 명시한다.
- `ios/`, `android/` 생성 여부와 소유권을 문서화한다.

## 설정

- app config 값은 typed config 또는 명확한 config 파일에서 관리한다.
- permission, scheme, intent filter, associated domain은 config plugin이나 native 설정과 함께 검증한다.
- EAS profile별 env와 build type을 구분한다.

## 의존성

- Expo SDK 버전과 React Native 버전 호환성을 확인한다.
- native module 추가 시 Expo Go 지원 여부를 명시한다.
