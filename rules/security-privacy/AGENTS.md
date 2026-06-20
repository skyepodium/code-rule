# 보안과 개인정보 규칙

이 디렉토리는 secret, 권한, 개인정보, 외부 SDK 규칙을 정의한다.

## secret

- secret, token, private key, service account JSON은 커밋하지 않는다.
- `.env.example`에는 실제 값 대신 placeholder를 둔다.
- public env prefix와 private env prefix를 구분한다.
- secret이 노출되면 코드 수정과 별개로 회전이 필요하다고 명시한다.

## 개인정보

- PII를 로그, analytics, crash report에 원문으로 남기지 않는다.
- 사용자 식별자는 필요한 범위에서만 전달하고 masking/hash 정책을 둔다.
- 권한 요청 문구는 필요한 기능과 사용 목적을 설명한다.

## 외부 SDK

- 외부 SDK 추가 전 수집 데이터, 권한, network endpoint, license를 확인한다.
- tracking, ads, analytics SDK는 opt-in/consent 요구사항을 검토한다.
- 보안 관련 로직은 client-only 검증에 의존하지 않는다.
