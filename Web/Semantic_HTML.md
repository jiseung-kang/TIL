# Semantic HTML

## Semantics

프로그래밍에서 `Semantics`는 `코드 조각의 의미`를 말한다.

> W3C에 따르면 "시맨틱 웹을 사용하면 애플리케이션, 기업 및 커뮤니티에서 데이터를 공유하고 재사용할 수 있다."

> Semantic, 즉 의미론적 요소는 브라우저와 개발자 모두에게 의미를 명확하게 설명한다.의미 없는 요소의 예 : <div>, <span> - 내용에 대해 알려주는 것이 없다.의미 요소의 예 : <form>, <table>, <article> - 내용을 명확하게 정의한다.

**`HTML`을 Semantic 콘텐츠 배포를 위한 강력한 도구로 생각하자!**

## Semantic HTML

> 예를 들어 HTML의 <h1> 요소는 의미론적 요소로,"페이지의 최상위 표제" 역할(또는 의미)을 감싸는 텍스트를 제공한다.
>
> ```
> <h1>05. Semantic HTML</h1>
> ```

이러한 태그는, 스타일에 한정적인 의미가 아닌 **의미론적** 가치를 지닌다.어떻게 보일 것인가(스타일)는 `CSS`의 책임이다.

### Semantic Markup의 이점

1. 검색 엔진 최적화(**[SEO](https://developer.mozilla.org/en-US/docs/Glossary/SEO)**)

- 검색 엔진은 콘텐츠를 페이지의 검색 순위에 영향을 미치는 중요한 키워드로 간주한다.

1. 웹 접근성 향상

- 스크린 리더는 시각 장애가 있는 사용자가 페이지를 탐색하는 데 도움이 되는 표지판으로 사용할 수 있습니다.

1. 탐색의 용이

- `의미 있는 코드 블록`을 찾는 것은 시맨틱 클래스나 네임스페이스 클래스가 있거나 없는 수많은 `div`들을 검색하는 것보다 훨씬 쉽다.

1. 채워질 데이터 유형을 개발자에게 제안한다.
2. 시맨틱 네이밍은 적절한 커스텀 요소/컴포넌트 네이밍을 반영한다.

## Semantic Elements

> 대략 100개의 의미론적 요소 중 일부에 대해 살펴보자

- `<section>`문서의 섹션. 섹션을 일반적으로 제목이 있는 콘텐츠의 주제별 그룹이다.사용 위치의 예 : 장, 소개, Article 항목, Contact 정보
- `<article>` - 자체로 의미가 있는 콘텐츠. 웹 사이트의 나머지 부분과 독립적이어야 한다.사용 위치의 예 : 게시물, 카드, 기사들
- `<header>`문서 또는 섹션의 머릿글을 정의한다.
- `<footer>` - 문서 또는 섹션의 바닥글을 정의한다.사용 위치의 예 : 저작권 정보, 연락처 정보, 사이트맵, 맨 위로 링크로 돌아가기, 관련 문서
- `<nav>` - 탐색 링크의 주요 블록에만 사용된다. 스크린 리더는 이 요소를 사용해 콘텐츠의 초기 렌더링을 생략할지 여부를 결정할 수 있다.
- `<aside>` - 배치된 콘텐츠 외에 일부 콘텐츠를 정의한다. 콘텐츠는 주변 콘텐츠와 간접적으로 관련되어야 한다.사용 위치의 예 : 사이드바
- `<figure>`, `<figcaption>` - `<figure>` 태그는 일러스트레이션, 다이어그램, 사진, 코드 목록 등과 같은 자체 포함된 콘텐츠를 지정한다. `<figcaption>` 태그는 요소에 대한 캡션을 정의한다. `<figure>` 요소는 `<figcaption>` 요소의 첫 번째 또는 마지막 자식으로 배치할 수 있다.사용 위치의 예 : 이미지 정의
- `<main>` - 문서의 기본 섹션. 고유한 콘텐츠. 검색 엔진 최적화에 유용하다. 단 하나만 있을 수 있다.봇이 페이지에 도달하면 `<main>`요소가 READ ME를 외친다!
- `<details>`
- `<mark>`
- `<summary>`
- `<time>`

## Semantic Markup의 예시와 사용 방법

![https://velog.velcdn.com/images/jiseung/post/ae611a79-f4b7-4557-822e-057bcd6086c2/image.png](https://velog.velcdn.com/images/jiseung/post/ae611a79-f4b7-4557-822e-057bcd6086c2/image.png)

![https://velog.velcdn.com/images/jiseung/post/618d272e-3a15-48b6-8b2a-359361bda82f/image.png](https://velog.velcdn.com/images/jiseung/post/618d272e-3a15-48b6-8b2a-359361bda82f/image.png)

![https://velog.velcdn.com/images/jiseung/post/a0c5ec40-6b7f-4a44-b936-1bc1443e94e6/image.png](https://velog.velcdn.com/images/jiseung/post/a0c5ec40-6b7f-4a44-b936-1bc1443e94e6/image.png)

> 태그를 남용하지는 말 것시맨틱 HTML 요소만 사용하더라도 남용하면 문서가 제대로 구성된 시맨틱 문서가 될 수 없다.

## 참고 링크

[Semantics](https://developer.mozilla.org/en-US/docs/Glossary/Semantics)[W3Schools: Semantic HTML](https://www.w3schools.com/html/html5_semantic_elements.asp)[How To Write Semantic HTML](https://hackernoon.com/how-to-write-semantic-html-dkq3ulo)
