# ESLint 규칙

이 디렉토리는 ESLint 설정과 검사 범위 규칙을 정의한다. 대상 프로젝트에서는 루트 또는 lint 설정 파일이 있는 디렉토리에 둔다.

## 필수 검사

- PR 전 `pnpm lint`를 통과해야 한다.
- TypeScript 프로젝트는 `pnpm typecheck`도 통과해야 한다.
- lint 대상은 직접 관리하는 앱 소스와 설정 파일로 한정한다.
- `dist`, `build`, `.next`, `coverage`, `node_modules`, generated 파일은 검사 대상에서 제외한다.

## 필수 규칙 의도

- 함수 선언문을 금지하고 화살표 함수 표현식을 강제한다.
- `any`를 금지한다.
- 매직 넘버와 매직 문자열 도입을 금지한다.
- 미사용 변수와 미사용 import를 금지한다.
- React hook 규칙을 강제한다.
- import 순서와 type-only import를 일관되게 유지한다.

## 권장 rule 모양

```js
{
  "func-style": ["error", "expression", { "overrides": { "namedExports": "expression" } }],
  "prefer-arrow-callback": "error",
  "@typescript-eslint/no-explicit-any": "error",
  "@typescript-eslint/no-unused-vars": "error",
  "@typescript-eslint/consistent-type-imports": "error",
  "no-magic-numbers": "off",
  "@typescript-eslint/no-magic-numbers": [
    "error",
    {
      "ignore": [0, 1, -1],
      "ignoreArrayIndexes": true,
      "ignoreEnums": false,
      "ignoreReadonlyClassProperties": false
    }
  ]
}
```

## disable 주석

- `eslint-disable`은 마지막 수단이다.
- disable 바로 위에는 한국어로 이유와 제거 조건을 적는다.
- 파일 전체 disable은 금지한다. 꼭 필요하면 별도 이슈나 PR로 분리한다.
- generated 파일은 disable 대신 ignore 범위에 넣는다.

## Next.js 프로젝트

- Next 공식 lint 설정 또는 프로젝트 표준 flat config 위에 팀 규칙을 얹는다.
- App Router 파일 convention 때문에 필요한 예외는 파일 glob 단위로 좁게 둔다.
- lint rule을 완화할 때는 어떤 코드 패턴 때문에 필요한지 예시를 남긴다.

