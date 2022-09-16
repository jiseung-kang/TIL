# FOUT, FIOT

## FOUT (Flash of Unstyled Tex)

기본 스타일을 먼저 적용하고, 웹 폰트가 다운로드되면 웹 폰트로 변환해 리렌더링하는 방식

- 장점 : 웹 폰트의 로딩 여부와 관련 없이 텍스트가 항상 보인다.
- 단점 : 글꼴의 자간, 높이 등 서식이 달라 웹 폰트 적용 전후의 레이아웃 차이가 존재할 수 있다.

## FOIT (Flash of Invisible Text)

웹 폰트가 다운로드 되고 나서 텍스트가 렌더링되는 방식

- 단점 : 웹 폰트가 로딩되지 않은지 3초가 지나면 fallback 폰트(기본 폰트)로 렌더링한다. 이러한 방식은 UX관점에서 좋지 않아 FOUT 방식으로 바꿔야 한다.

## FOUT 해결 방법

1. Font Face Observer
   폰트 로딩 성공 시 promise 객체를 리턴해주는 라이브러리.
   promise 반환 결과에 따라 class를 추가해 FOUT처럼 작동되도록 할 수 있다.

2. font-display 방식
   font-display 속성을 이용해 FOUT처럼 보이게 할 수 있다.

- block : FOIT처럼 동작
- swap : FOUT처럼 동작
- fallback : 100ms 이후 fallback 폰트로 렌더링. 2초 간의 swap 전환 시간이 존재해 이때 변환되지 않으면 웹 폰트로 변환되지 않는다.
- optional : fallback과 비슷하지만 네트워크 상태를 파악해 네트워크 상태가 좋지 않으면 캐시에만 저장하고 페이지에 적용하지 않는다.

font-display 방식은 FOIT가 사용되는 대표적인 브라우저들에서는 작동하지만 CSS로 설정에 한계가 존재한다. (swap time, block time을 조절할 수 없어 한글 폰트를 다운 받기 힘들다.)

## FOUT 해결 방법

폰트가 로딩되지 않았을 때 기본 폰트로 레이아웃이 달라질 수 있다.

- font style matcher
  두 폰트 사이의 간격을 조정하고 font observer 라이브러리의 폰트 로더 방법으로 디테일하게 기본 폰트의 속성을 이용하고자 하는 폰트의 속성과 맞춰준다.
