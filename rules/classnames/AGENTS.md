# classnames Rules

This directory defines React `className` composition rules. In target projects, place it in directories with many JSX files, such as `components/`, `ui/`, or `src/`.

## Basic Principles

- Use `classnames` for conditional class composition.
- Standardize the import name as `classNames`.
- Static class strings may stay inline.
- If any condition is involved, compose with `classNames(...)`.
- Do not create conditional classes with string addition, template literals, or array `join`.

## Example

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

  return <button className={buttonClassName}>Save</button>;
};

export { Button };
```

## CSS Modules

- Files using CSS Modules must use `classnames/bind`.
- Use `cx` only within the file; do not export it.
- CSS Module keys must match the actual classes in the styles file.

```tsx
import bindClassNames from "classnames/bind";
import styles from "./Button.module.css";

const cx = bindClassNames.bind(styles);
```

## Forbidden Patterns

- Do not add strings like `base + " " + activeClass`.
- Do not use conditional template literals like `` `${base} ${isActive ? active : ""}` ``.
- Do not use patterns like `[base, isActive && active].filter(Boolean).join(" ")`.
- Do not hide state names inside class strings. Write state variable names and class keys so they can be read together.

## Exceptions

- If the design system already provides a `cn` wrapper, use that wrapper.
- In projects that need Tailwind merge, handle it only inside `cn`; call sites follow the same rules.
