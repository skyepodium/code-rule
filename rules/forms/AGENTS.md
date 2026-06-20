# Form 규칙

이 디렉토리는 form state, validation, submit 규칙을 정의한다.

## 상태

- field value, touched, dirty, error, submit state를 구분한다.
- validation schema 또는 명시적 validator를 사용한다.
- server validation error와 client validation error를 구분한다.
- form state를 불필요하게 global store에 올리지 않는다.

## 입력

- input label, placeholder, helper text, error text 역할을 섞지 않는다.
- 숫자, 날짜, 통화, 전화번호는 parse와 display formatting을 분리한다.
- IME composition과 모바일 keyboard type을 고려한다.

## 제출

- submit 중복 실행을 막는다.
- submit 실패 시 사용자가 복구할 수 있는 메시지를 제공한다.
- 성공 후 reset, navigation, optimistic update 기준을 명시한다.
