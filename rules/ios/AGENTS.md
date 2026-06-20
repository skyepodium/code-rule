# iOS 규칙

이 디렉토리는 iOS native 코드와 설정 규칙을 정의한다.

## Info.plist와 권한

- permission usage description은 기능 목적을 명확히 설명한다.
- entitlement, background mode, capability 추가 시 필요성과 배포 영향을 문서화한다.
- private API에 의존하지 않는다.

## Swift/Objective-C

- AppDelegate/SceneDelegate는 bootstrap과 wiring만 담당한다.
- native bridge는 작은 module로 나누고 JS contract를 명시한다.
- thread, callback, observer는 lifecycle에 맞춰 정리한다.
- UI 시각 값은 token/resource 경계를 통해 사용한다.

## 배포

- bundle id, signing, provisioning 변경은 별도 위험으로 기록한다.
- background execution은 Apple이 허용하는 mode 안에서만 설계한다.
