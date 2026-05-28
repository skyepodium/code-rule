# Next.js 규칙

이 디렉토리는 Next.js App Router 프로젝트 규칙을 정의한다. 대상 프로젝트에서는 `app/` 또는 `src/app/` 아래에 둔다.

## 라우팅 모델

- App Router를 기본으로 사용한다.
- `pages/` 라우터와 App Router를 새 기능에서 섞지 않는다.
- `page.tsx`는 화면 조립, `layout.tsx`는 공통 레이아웃, `route.ts`는 HTTP 경계만 담당한다.
- `loading.tsx`, `error.tsx`, `not-found.tsx`는 해당 segment의 상태 UI만 담당한다.

## 서버 컴포넌트와 클라이언트 컴포넌트

- 서버 컴포넌트를 기본값으로 한다.
- `"use client"`는 상호작용, browser API, React state/effect가 필요한 가장 작은 leaf 컴포넌트에만 둔다.
- 클라이언트 컴포넌트 props는 직렬화 가능한 값만 받는다.
- 서버 전용 코드, secret, database client는 클라이언트 번들로 들어가지 않게 분리한다.
- provider는 가능한 깊게 배치해 정적 서버 렌더링 범위를 넓힌다.

## 데이터 접근

- 서버에서 가져올 수 있는 데이터는 서버 컴포넌트, server action, route handler에서 가져온다.
- 클라이언트에서 직접 외부 API secret을 다루지 않는다.
- `fetch` cache, revalidate, runtime 설정은 파일 상단 상수로 명시하고 매직 넘버를 남기지 않는다.
- 요청과 응답 타입은 명시하고 외부 응답은 검증 후 사용한다.

## 라우트 핸들러

- 라우트 핸들러 파일명은 `route.ts`를 사용한다.
- 함수 선언문 대신 `export const GET = async (...) => {}`처럼 화살표 함수 표현식으로 작성한다.
- `NextApiRequest`, `NextApiResponse`는 App Router route handler에서 사용하지 않는다.
- 응답 상태 코드, cache TTL, header 이름은 상수화한다.
- 여러 HTTP method가 한 파일에 있으면 공통 로직을 순수 함수로 분리한다.

## 메타데이터와 SEO

- 정적 메타데이터는 `metadata` export로 둔다.
- 동적 메타데이터는 `generateMetadata`를 화살표 함수 표현식으로 작성한다.
- title, description, Open Graph 문자열이 반복되면 상수 또는 config로 분리한다.

## Next 내장 컴포넌트

- 내부 이동은 `next/link`를 사용한다.
- 이미지 최적화가 필요한 이미지에는 `next/image`를 우선 사용한다.
- 폰트는 Next font 또는 프로젝트 표준 로딩 경로를 따른다.

