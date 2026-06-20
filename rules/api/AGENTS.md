# API 규칙

이 디렉토리는 HTTP/API client, schema 검증, retry 규칙을 정의한다.

## 경계

- API 호출은 adapter 또는 service 경계에 둔다.
- UI 컴포넌트는 fetch 세부 구현, header, raw endpoint를 직접 다루지 않는다.
- endpoint path, header key, query key, timeout은 상수화한다.
- request/response 타입은 명시하고 외부 응답은 검증 후 도메인 타입으로 변환한다.

## 실패 처리

- network error, timeout, 인증 실패, validation 실패를 구분한다.
- retry는 idempotent 요청 위주로 적용하고 retry count/backoff는 상수화한다.
- 인증 갱신과 재요청 흐름은 한 경계에 모아 중복 구현하지 않는다.

## 데이터 모델

- API DTO와 UI view model을 섞지 않는다.
- 서버 enum/string union은 unknown 가능성을 처리한다.
- 날짜, 숫자, 통화, 단위는 parse와 formatting 경계를 분리한다.
