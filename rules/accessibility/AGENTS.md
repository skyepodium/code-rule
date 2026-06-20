# 접근성 규칙

이 디렉토리는 UI 접근성 기본 규칙을 정의한다.

## 기본

- 상호작용 요소는 접근성 label과 role을 가진다.
- icon-only 버튼은 보이는 tooltip 또는 접근성 label을 제공한다.
- disabled/loading 상태는 시각 상태와 accessibility state에 함께 반영한다.
- 중요한 상태 변화는 screen reader가 알 수 있는 경로를 둔다.

## 입력과 포커스

- form field는 label, error, hint 관계를 명확히 한다.
- modal, drawer, dialog는 focus trap과 닫기 동작을 가진다.
- keyboard navigation 순서는 화면의 시각 순서와 일치해야 한다.

## 시각

- 텍스트 대비를 확인하고 토큰으로 관리한다.
- touch target은 플랫폼 권장 최소 크기를 만족한다.
- motion은 reduced motion 설정을 존중한다.
