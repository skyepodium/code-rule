# Git 규칙

이 디렉토리는 branch, commit, history hygiene 규칙을 정의한다.

## branch

- 기본 PR 대상 브랜치는 루트 규칙 또는 프로젝트 규칙을 따른다.
- 작업 브랜치는 기능, 수정, 문서 작업 의도가 드러나게 이름 짓는다.
- unrelated change를 같은 commit/PR에 섞지 않는다.

## commit

- commit message는 변경 의도가 드러나게 작성한다.
- generated file, lockfile, migration은 관련 source change와 함께 커밋한다.
- 실패한 실험, 임시 로그, 주석 처리된 코드는 커밋하지 않는다.

## 안전

- `git reset --hard`, `git checkout --`, force push는 명시적 요청 없이 하지 않는다.
- 다른 사람이 만든 변경을 되돌리지 않는다.
- 충돌 해결은 어떤 쪽을 선택했는지 근거를 남긴다.
