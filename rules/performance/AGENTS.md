# Performance 규칙

이 디렉토리는 render, bundle, list, native bridge 성능 규칙을 정의한다.

## 렌더링

- memoization은 측정 가능한 re-render 비용이 있을 때 사용한다.
- 큰 계산은 render path에서 분리하고 필요하면 memoized selector를 사용한다.
- inline 객체/함수 최적화는 실제 문제가 있을 때 적용한다.

## 리스트와 데이터

- 큰 리스트는 virtualization을 사용한다.
- pagination, page size, prefetch threshold는 상수화한다.
- 이미지와 asset은 필요한 크기로 로드한다.

## bridge와 IO

- native bridge 호출은 빈도와 payload 크기를 제한한다.
- polling interval, debounce, throttle 값은 상수화한다.
- 성능 개선은 before/after 측정 또는 재현 가능한 증거를 남긴다.
