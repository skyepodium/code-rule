# Config 규칙

이 디렉토리는 환경 변수, runtime config, feature flag 규칙을 정의한다.

## 환경 변수

- env 이름은 영어 대문자와 `_`를 사용한다.
- public client env와 private server env prefix를 구분한다.
- `.env.example` 또는 문서에 필요한 key와 의미를 기록한다.
- env 값은 startup 경계에서 검증하고 typed config로 변환한다.

## runtime/build config

- build-time config와 runtime config를 섞지 않는다.
- platform별 config는 adapter나 platform config 파일로 분리한다.
- config 기본값은 상수화하고 숨은 fallback을 만들지 않는다.

## feature flag

- flag 이름, owner, 제거 조건을 문서화한다.
- 임시 flag는 제거 시점을 명시한다.
- flag 분기는 가능한 경계 컴포넌트나 service에 모은다.
