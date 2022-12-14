# 브라우저의 렌더링 과정

- 구글의 V8 자바스크립트 엔진으로 빌드된 자바스크립트 런타임 환경인 Node.js의 등장
- 애플리케이션 개발까지 가능한 범용 개발 언어가 되었다.
- 대부분의 프로그래밍 언어는 운영체제나 가상 머신 위에서 실행하지만
- 자바스크립트는 브라우저에서 HTML, CSS와 함께 실행

## 브라우저에 렌더링하는 법

- 파싱
  - 구문 분석
  - 토큰으로 분해하고 파스 트리를 생성하는 일련의 과정
  - 파스 트리를 기반으로 중간 언어인 바이트코드를 생성하고 실행한다.
- 렌더링
  - 브라우저에 시각적으로 출력

1. HTML, CSS, 자바스크립트, 이미지, 폰트 파일 등 렌더링에 필요한 리소스를 요청하고 서버로부터 응답받는다.
2. 브라우저의 렌더링 엔진은 서버로부터 응답된 HTML과 CSS를 파싱해 DOM, CSSOM을 생성하고 이들을 결합해 렌더 트리를 생성한다.
3. 브라우저의 자바스크립트 엔진은 서버로부터 응답된 자바스크립트를 파싱해 AST를 생성하고 바이트코드로 변환하여 실행한다. 이때 자바스크립트는 DOM API를 통해 DOM이나 CSSOM을 변경할 수 있다. 변경된 DOM과 CSSOM은 다시 렌더 트리로 결합된다.
4. 렌더 트리를 기반으로 HTML 요소의 레이아웃을 계산하고 브라우저 화면에 HTML 요소를 페인팅한다.

## 요청과 응답

브라우저의 핵심 기능은 필요한 리소스(HTML, CSS, 자바스크립트, 이미지, 폰트 등 정적 파일 또는 서버가 동적으로 생성한 데이터)를 서버에 요청하고 서버로부터 응답받아 브라우저에 시각적으로 렌더링하는 것

렌더링에 필요한 리소스는 모두 서버에 존재한다. 필요한 리소스를 서버에 요청하고 서버가 응답한 리소스를 파싱해 렌더링하는 것

서버에 요청을 전송하기 위해 브라우저는 주소창을 제공한다.

브라우저 주소창에 URL을 입력하고 엔터 키를 누르면 URL의 호스트 이름이 DNS를 통해 IP주소로 변환되고 이 IP 주소를 갖는 서버에 요청을 전송한다.

서버는 루트 요청에 대해 서버의 루트 폴더에 존재하는 정적 파일 index.html을 클라이언트(브라우저)로 응답한다. 다른 html 요청 시 정적 파일의 경로를 기술해 요청한다.

자바스크립트를 통해서도 서버에 정적/동적 데이터를 요청할 수 있다.

요청과 응답은 개발자 도구의 Network 패널에서 확인할 수 있다.

## HTTP 1.1과 HTTP 2.0

HTTP는 웹에서 브라우저와 서버가 통신하기 위한 프로토콜

- HTTP/1.1
  - 기본적으로 커넥션 당 하나의 요청과 응답만 처리한다.
  - 리소스 요청이 개별적으로 전송되고 응답도 개별적으로 전송된다.
  - 리소스 동시 전송이 불가능해 요청할 리소스의 개수에 비례해 응답 시간도 증가하는 단점이 있다.
- HTTP
  - 커넥션당 여러 개의 요청과 응답이 가능하다.
  - 다중 요청/응답이 가능해 리소스의 동시 전송이 가능하므로 페이지 로드 속도가 더 빠르다.

## HTML 파싱과 DOM 생성

순수한 텍스트인 HTML을 브라우저가 이해할 수 있는 자료구조(객체)로 변환해 메모리에 저장해야 한다.

DOM : 브라우저가 이해할 수 있는 자료구조

1. 서버에 존재하던 HTML 파일이 브라우저의 요청에 의해 응답된다. 서버는 HTML 파일을 읽어 들여 메모리에 저장한 다음 메모리에 저장된 바이트를 인터넷을 경유해 응답한다.
2. 브라우저는 서버가 응답한 HTML 문서를 바이트로 응답받고, meta 태그의 charset 어트리뷰트에 의해 지정된 인코딩 방식을 기준으로 문자열로 변환된다. meta 태그는 응답 헤더에 담겨 온다.
3. 문자열로 변환된 HTML 문서를 읽어 들여 문법적 의미를 갖는 코드의 최소 단위 토큰으로 분해된다.
4. 각 토큰들을 객체로 변환해 노드를 생성한다. 내용에 따라 문서 노드, 요소 노드, 어트리뷰트 노드, 텍스트 노드가 되며 이들은 DOM을 구성하는 기본 요소가 된다.
5. HTML 문서는 HTML 요소들의 집합으로 이루어지며 HTML 요소는 중첩 관계를 갖는다. 즉 HTML 요소의 콘텐츠 영역에는 텍스트뿐만 아니라 다른 HTML 요소도 포함될 수 있다. 이 중첩 관계를 반영해 트리 자료구조가 구성되며 이것을 DOM이라 부른다.

## CSS 파싱과 CSSOM 생성

렌더링 엔진은 HTML을 처음부터 한 줄씩 순차적으로 파싱해 DOM을 생성해 나간다.

렌더링엔진은 DOM을 생성해가다가 CSS를 로드하는 link, style 태그를 만나면 DOM 생성을 일시 중단한다.

link 태그의 href 어트리뷰트에 지정된 CSS 파일을 서버에 요청해 로드한 CSS, style 태그 내의 CSS를 HTML처럼 파싱(바이트 - 문자 - 토큰 - 노드 - CSSOM)을 거쳐 해석해 CSSOM을 생성한다.

CSS 파싱을 완료하면 HTML 파싱이 중단된 지점부터 다시 HTML을 파싱하기 시작해 DOM 생성을 재개한다.

> CSSOM은 CSS 상속을 반영해 생성된다.

## 렌더 트리 생성

렌더링 엔진은 서버로부터 응답된 HTML과 CSS를 파싱해 각각 DOM과 CSSOM을 생성한다.

그리고 DOM과 CSSOM은 렌더 트리로 결합된다.

렌더 트리는 렌더링을 위한 트리 구조의 자료구조

브라우저 화면에 렌더링되지 않는 노드와 CSS에 의해 비표시되는 노드들을 포함하지 않는다.

완성된 렌더 트리는 각 HTML 요소의 레이아웃을 계산하는 데 사용되며 브라우저 화면에 픽셀을 렌더링하는 페인팅 처리에 입력된다.

- 다음의 경우 레이아웃 계산, 페인팅이 실행된다.
  - 노드 추가 삭제
  - 브라우저 리사이징에 의한 뷰포트 크기 변경
  - HTML 요소의 레이아웃에 변경을 발생시키는 스타일 변경

이런 리렌더링은 비용이 많이 들고, 성능에 악영향을 준다.

## 자바스크립트 파싱과 실행

HTML 문서를 파싱한 결과물로 생성된 DOM과 HTML 문서의 구조와 정보뿐만 아니라 HTML 요소와 스타일 등을 변경할 수 있는 프로그래밍 인터페이스로서 DOM API를 제공한다.

DOM API를 사용해 이미 생성된 DOM을 동적으로 조작할 수 있다.

렌더링 엔진은 HTML을 한 줄씩 순차적으로 파싱해 DOM을 생성해 나가다가 script 태그를 만나면 일시 중단하고

src 어트리뷰트에 정의된 자바스크립트 파일을 서버에 요청해 로드한 자바스크립트 파일이나 script 태그 내의 자바스크립트 코드를 파싱하기 위해 자바스크립트 엔진에 제어권을 넘긴다.

이후에 다시 중단 시점부터 DOM 생성을 재개한다.

자바스크립트 파싱과 실행은 브라우저의 렌더링 엔진이 아닌 자바스크립트 엔진이 처리한다.

자바스크립트 엔진을 자바스크립트 코드를 파싱해 CPU가 이해할 수 있는 저수준 언어로 변환하고 실행한다.

자바스크립트 엔진은 구글 크롬과 Node.js의 V8, 파이어폭스의 SpiderMonkey, 사파리의 JavaScriptCore 등 다양한 종류가 있다.

자바스크립트 엔진은 AST를 생성한다. 그리고 AST를 기반으로 인터프리터가 실행할 수 있는 중간 코드인 바이트코드를 생성해 실행한다.

- 토크나이징
  - 자바스크립트 소스코드를 어휘 분석해 토큰들로 분해한다. 이 과정을 렉싱이라고 부르기도 하지만 조금 다르다.
- 파싱
  - 토큰들의 집합을 구문 분석해 AST를 생성한다. AST는 토큰에 문법적 의미와 구조를 반영한 트리 구조의 자료구조
  - AST를 사용해 TypeScript, Babel, Prettier 등 트랜스파일러를 구현할 수도 있다.
- 바이트코드 생성과 실행
  - 파싱의 결과 AST는 바이트 코드로 변환되어 인터프리터에 의해 실행된다.
  - V8 엔진은 자주 사용되는 코드가 터보팬(컴파일러)에 의해 최적화된 머신 코드로 컴파일되어 성능을 최적화한다. 디옵티마이징하기도 한다.

## 리플로우와 리페인트

DOM API가 사용된 경우 DOM이나 CSSOM이 변경된다.

그리고 다시 렌더 트리로 결합되고 페인트 과정을 거쳐 렌더링된다.

리플로우 : 레이아웃 계산을 다시한다.

리페인트 : 다시 페인트하는 것

## 자바스크립트 파싱에 의한 HTML 파싱 중단

렌더링 엔진과 자바스크립트 엔진은 직렬적으로, 동기적으로 파싱을 수행한다. 즉 블로킹이 일어난다.

script 태그의 위치가 중요한 이유이다.

- 자바스크립트 로딩/파싱/실행으로 인해 HTML 렌더링에 지장받는 일이 발생하지 않아 페이지 로딩 시간이 빨라진다.

## script 태그의 async/defer 어트리뷰트

이걸 사용하면 비동기적으로 동시 실행이 가능하다.

- async
  - 자바스크립트의 파싱과 실행은 자바스크립트 파일의 로드가 완료된 직후 실행된다.
  - 이때 HTML 파싱이 중단된다.
  - 여러 개에 async를 사용하면 순서가 보장되지 않는다.
- defer
  - 자바스크립트의 파싱과 실행은 HTML 파싱이 완료된 직후(DOMContentLoaded) 진행된다.
