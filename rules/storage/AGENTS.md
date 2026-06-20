# Storage 규칙

이 디렉토리는 local storage, secure storage, cache 저장 규칙을 정의한다.

## key와 schema

- storage key는 도메인 상수로 관리한다.
- 저장 값은 version 또는 schema를 가진다.
- 읽을 때 외부 입력으로 보고 `unknown`에서 검증 후 도메인 타입으로 변환한다.
- parse 실패 시 fallback, migration, 삭제 중 하나의 전략을 명시한다.

## 민감 정보

- access token, refresh token, 개인 식별 정보는 일반 storage에 저장하지 않는다.
- 민감 정보는 secure storage/keychain/keystore 같은 플랫폼 보안 저장소를 사용한다.
- 로그와 analytics에 storage 원문 값을 남기지 않는다.

## lifecycle

- cache는 TTL, invalidation, reset 기준을 가진다.
- logout, 계정 전환, workspace 전환 시 지워야 할 key를 명시한다.
- 테스트에서 초기화하기 어려운 전역 storage wrapper는 만들지 않는다.
