# Logging과 Observability 규칙

이 디렉토리는 로그, analytics, crash reporting 규칙을 정의한다.

## logging

- production 코드에서 임의의 `console.log`를 남기지 않는다.
- logger wrapper를 사용하고 level, domain, context를 명시한다.
- PII, token, raw credential, 민감 payload를 로그에 남기지 않는다.
- catch에서 로깅할 때는 복구 여부와 사용자 영향도를 함께 드러낸다.

## analytics

- event name과 property key는 상수화한다.
- analytics event는 사용자 행동 또는 제품 질문과 연결되어야 한다.
- 중복 event와 render 기반 자동 발화를 피한다.
- consent가 필요한 event는 동의 상태를 확인한다.

## crash/reporting

- error boundary와 crash reporter는 bootstrap 경계에서 연결한다.
- non-fatal error는 actionability가 있을 때만 보고한다.
- release version, build number, platform context를 함께 보낸다.
