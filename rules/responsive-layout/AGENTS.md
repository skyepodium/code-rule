# 반응형 레이아웃 규칙

이 디렉토리는 화면 크기, safe area, overflow 규칙을 정의한다.

## 레이아웃

- 고정 width/height는 fixed-format UI에만 사용하고 responsive constraint를 함께 둔다.
- 화면 padding, gap, breakpoint는 디자인 토큰으로 관리한다.
- safe area, notch, status bar, navigation bar 영역을 고려한다.
- keyboard가 뜨는 화면은 입력 필드와 submit 버튼이 가려지지 않게 설계한다.

## 텍스트

- 텍스트가 컨테이너를 넘치거나 다른 UI를 덮지 않게 한다.
- 긴 단어, 번역 문자열, dynamic type을 고려한다.
- viewport width에 직접 비례해 font size를 조절하지 않는다.

## 상태

- loading, empty, error 상태에서도 레이아웃 shift가 과도하지 않게 한다.
- hover/focus/pressed 상태가 요소 크기를 바꾸지 않게 한다.
