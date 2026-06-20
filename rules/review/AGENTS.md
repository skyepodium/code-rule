# Review 규칙

이 디렉토리는 self-review, PR review, review 대응 규칙을 정의한다.

## self-review

- PR 전 diff를 직접 읽고 의도하지 않은 파일 변경을 제거한다.
- public API, migration, config, permission, dependency 변경을 별도로 확인한다.
- 새 규칙 위반을 발견하면 같은 작업 범위에서 고친다.

## PR 내용

- 구현 의도, 주요 변경, 검증 결과, 남은 위험을 적는다.
- 스크린샷이나 영상이 필요한 UI 변경은 evidence를 첨부한다.
- AI가 참여한 경우 루트 PR 규칙의 participant 섹션을 따른다.

## review 대응

- review comment를 그대로 수용하기 전에 기술적으로 검증한다.
- 반영하지 않는 의견은 근거를 짧게 남긴다.
- fix 후 관련 테스트나 검증 명령을 다시 실행한다.
