# Storybook 규칙

이 디렉토리는 컴포넌트 story와 시각 문서화 규칙을 정의한다.

## story 범위

- 재사용 UI 컴포넌트는 기본, loading, disabled, error, empty 상태 story를 둔다.
- form control은 validation/error/focus 상태를 포함한다.
- 디자인 토큰이나 theme 변화가 있으면 대표 story로 확인한다.

## 작성

- story args는 실제 props 타입과 일치해야 한다.
- mock data는 named fixture로 관리한다.
- story 안에 API 호출이나 production side effect를 넣지 않는다.

## 검증

- visual regression 대상 story는 변동성 있는 시간, 랜덤, animation을 고정한다.
- 접근성 addon이나 수동 체크로 기본 label/role을 확인한다.
