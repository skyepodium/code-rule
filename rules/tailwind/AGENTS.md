# Tailwind 규칙

이 디렉토리는 Tailwind class와 token 사용 규칙을 정의한다.

## class 작성

- 조건부 class 조합은 `classnames` 또는 프로젝트 표준 `cn` wrapper를 사용한다.
- arbitrary value는 디자인 토큰에 없는 일회성 예외에만 사용하고 이유를 남긴다.
- 긴 className은 의미 있는 컴포넌트나 variant helper로 분리한다.

## token

- 색상, spacing, radius, typography는 Tailwind config와 디자인 토큰을 맞춘다.
- raw hex color를 className arbitrary value로 직접 쓰지 않는다.
- variant 이름은 시각 값보다 의미를 드러낸다.

## 금지

- 조건부 template literal로 className을 조립하지 않는다.
- Tailwind class와 inline style에 같은 시각 값을 중복 정의하지 않는다.
