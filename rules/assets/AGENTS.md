# Asset 규칙

이 디렉토리는 이미지, 아이콘, 폰트, 앱 asset 관리 규칙을 정의한다.

## 파일

- asset 파일명은 영어와 kebab-case를 사용한다.
- 기능/브랜드/플랫폼별 디렉토리로 나누고 임의의 `images/` 폴더에 모두 넣지 않는다.
- 원본과 generated asset을 구분한다.
- 큰 바이너리 asset 추가 전 크기와 사용처를 확인한다.

## 이미지와 아이콘

- 아이콘은 기존 icon system이나 library를 우선 사용한다.
- 같은 의미의 아이콘을 중복 추가하지 않는다.
- 이미지 크기, density, format은 플랫폼 요구사항에 맞춘다.
- decorative image와 content image를 구분해 접근성 처리한다.

## 폰트

- 폰트 파일 추가 전 license와 subset 필요성을 확인한다.
- font family 이름과 weight mapping을 문서화한다.
