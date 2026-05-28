# classnames 규칙

이 디렉토리는 React `className` 조합 규칙을 정의한다. 대상 프로젝트에서는 `components/`, `ui/`, `src/`처럼 JSX가 많은 디렉토리에 둔다.

## 기본 원칙

- 조건부 class 조합은 `classnames`를 사용한다.
- import 이름은 `classNames`로 통일한다.
- 정적 class 문자열은 인라인으로 둘 수 있다.
- 조건이 하나라도 들어가면 `classNames(...)`로 조합한다.
- 문자열 덧셈, template literal, 배열 `join`으로 조건부 class를 만들지 않는다.

## 사용 예시

```tsx
import classNames from "classnames";

type ButtonProps = {
  isActive: boolean;
  className?: string;
};

const Button = ({ isActive, className }: ButtonProps) => {
  const buttonClassName = classNames(
    "button",
    {
      "button-active": isActive,
    },
    className,
  );

  return <button className={buttonClassName}>저장</button>;
};

export { Button };
```

## CSS Modules

- CSS Modules를 쓰는 파일은 `classnames/bind`를 사용한다.
- `cx`는 파일 내부에서만 사용하고 export하지 않는다.
- CSS Module key는 styles 파일의 실제 class와 일치해야 한다.

```tsx
import bindClassNames from "classnames/bind";
import styles from "./Button.module.css";

const cx = bindClassNames.bind(styles);
```

## 금지 패턴

- `base + " " + activeClass`처럼 문자열을 더하지 않는다.
- `` `${base} ${isActive ? active : ""}` ``처럼 조건부 template literal을 쓰지 않는다.
- `[base, isActive && active].filter(Boolean).join(" ")` 패턴을 쓰지 않는다.
- 상태 이름을 class 문자열 안에 숨기지 않는다. 상태 변수명과 class key가 함께 읽히게 작성한다.

## 예외

- 디자인 시스템이 `cn` wrapper를 이미 제공하면 그 wrapper를 사용한다.
- Tailwind merge가 필요한 프로젝트는 `cn` 내부에서만 처리하고 호출부는 동일한 규칙을 따른다.

