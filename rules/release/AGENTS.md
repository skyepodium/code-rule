# Release 규칙

이 디렉토리는 versioning, changelog, artifact, rollout 규칙을 정의한다.

## versioning

- version bump 기준을 프로젝트 release policy에 맞춘다.
- 앱은 versionName/versionCode 또는 build number 변경을 추적한다.
- package는 public API 변경과 semver 영향을 기록한다.

## changelog

- 사용자 영향이 있는 변경은 changelog나 release note에 남긴다.
- breaking change는 migration note를 포함한다.
- 내부 refactor만 있는 경우 사용자 문구를 과장하지 않는다.

## rollout

- release artifact 생성 명령과 검증 명령을 문서화한다.
- staged rollout, rollback, hotfix 기준을 명시한다.
- 배포 전 lint, typecheck, test, build evidence를 확인한다.
