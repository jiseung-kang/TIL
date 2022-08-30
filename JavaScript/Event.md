# 이벤트

## 이벤트 드리븐 프로그래밍

이벤트 핸들러 : 이벤트가 발생했을 때 호출될 함수

이벤트 핸들러 등록 : 이벤트 발생 시 브라우저에게 이벤트 핸들러의 호출을 위임하는 것

이벤트 핸들러 프로퍼티에 함수를 할당하면 해당 이벤트가 발생했을 때 할당한 함수가 브라우저에 의해 호출된다.

> 이벤트와 이벤트 핸들러를 통해 사용자와 애플리케이션이 상호작용하는 프로그래밍 방식을 이벤트 드리븐 프로그래밍이라고 한다.

## 이벤트 타입

이벤트 타입 : 이벤트의 종류를 나타내는 문자열

- 마우스 이벤트
  - click
  - dblclick
  - mousedown
  - mouseup
  - mousemove
  - mouseenter (버블링X)
  - mouseover (버블링O)
  - mouseleave (버블링X)
  - mouseout (버블링O)
- 키보드 이벤트
  - keydown
  - keypress
  - keyup
- 포커스 이벤트
  - focus (버블링X)
  - blur (버블링X)
  - focusin (버블링O)
  - focusout (버블링O)
- 폼 이벤트
  - submit
  - reset
- 값 변경 이벤트
  - input
  - change
  - readystatechange
- DOM 뮤테이션 이벤트
  - DOMContentLoaded
- 뷰 이벤트
  - resize
  - scroll
- 리소스 이벤트
  - load
  - unload
  - abort
  - error

## 이벤트 핸들러 등록

이벤트 핸들러 : 이벤트가 발생했을 때 브라우저에 호출을 위임한 함수

이벤트가 발생하면 브라우저에 의해 호출될 함수

### 이벤트 핸들러 어트리뷰트 방식

이벤트에 대응하는 이벤트 핸들러 어트리뷰트(onclick 등)

> 이벤트 핸들러 어트리뷰트 값은 암묵적으로 생성될 이벤트 핸들러의 함수 몸체를 의미한다.

HTML과 자바스크립트는 관심사가 다르므로 분리하는 것이 좋다.

하지만 CBD 방식의 프레임워크, 라이브러리에서는 이 방식을 쓰기도 하는데,

CBD에서는 HTML, CSS, JavaScript를 뷰를 구성하기 위한 요소로 보기 때문이다.

### 이벤트 핸들러 프로퍼티 방식

이벤트 핸들러 프로퍼티에 이벤트 핸들러를 바인딩하면 이벤트 핸들러가 등록된다.

이벤트타깃.on이벤트타입 = 이벤트 핸들러

> 이벤트 핸들러는 이벤트 타깃, 또는 전파된 이벤트를 캐치할 DOM 노드 객체에 바인딩한다.

이 방식은 HYML과 자바스크립트가 뒤섞이는 문제를 해결하지만

하나의 이벤트 핸들러만 바인딩할 수 있다는 단점이 있다.

### addEventListener 메서드 방식

`EventTarget.prototype.addEventListener(’eventType’, functionName, [, useCapture]);`

마지막 매개변수에 이벤트를 캐치할 이벤트 전파 단계(캡쳐링 또는 버블링)를 지정한다.

생략, false : 버블링 단계

true : 캡쳐링 단계

참조가 동일한 이벤트 핸들러를 중복 등록하면 하나의 핸들러만 등록된다.

## 이벤트 핸들러 제거

`EventTarget.prototype.removeEventListener`

무명 함수를 이벤트 핸들러로 등록하면 제거할 수 없다.

기명 함수를 등록할 수 없다면 arguments.callee를 사용할 수 있지만 strict mode에서 금지된다.

프로퍼티에는 null을 할당할 수 있다.

## 이벤트 객체

이벤트 발생 시 동적으로 이벤트 객체가 생성되어 이벤트 핸들러의 첫번째 인수로 전달된다.

이벤트 핸들러 어트리뷰트 방식의 경우 무조건 event로 매개변수 이름을 지어야 한다.

### 이벤트 객체의 공통 프로퍼티

type, target, currentTarget, eventPhase, bubbles, cancelable, defaultPrevented, isTrusted, timeStamp

target : 이벤트를 발생시킨 객체

currentTarget: 이벤트 핸들러가 바인딩된 DOM 요소

### 마우스 정보 취득

click, dblclick, mousedown, mouseup, mousemove, mouseenter, mouseleave

### 키보드 정보 취득

keydown, keyup, keypress

input 요소의 입력 필드에 한글을 입력하고 엔터를 누르면 keyup 이벤트 핸들러가 두 번 호출되므로 keydown 이벤트를 캐치하자.

## 이벤트 전파

DOM 트리 상에 존재하는 DOM 요소 노드에서 발생한 이벤트는 DOM 트리를 통해 전파된다.

이를 이벤트 전파라고 부른다.

이벤트 발생 시 생성된 이벤트 객체는 이벤트를 발생시킨 이벤트 타깃을 중심으로 DOM 트리를 통해 전파된다.

- 캡처링 단계 : 이벤트가 상위 요소에서 하위 요소 방향으로 전파
- 타깃 단계 : 이벤트가 이벤트 타깃에 도달
- 버블링 단계 : 이벤트가 하위 요소에서 상위 요소 방향으로 전파

이벤트 핸들러 어트리뷰트/프로퍼티 방식 이벤트 핸들러는 타깃 단계, 버블링 단계의 이벤트만 캐치할 수 있다.

addEventListener 메서드로 등록된 이벤트 핸들러는 타깃 단꼐, 버블링 단계, 캡처링 단계의 이벤트를 캐치할 수 있다. (true)

> 이벤트는 이벤트를 발생시킨 이벤트 타깃은 물론 상위 DOM 요소에서도 캐치할 수 있다.

Event.prototype.composedPath

이벤트는 캡처링 - 타깃 - 버블링 단계로 전파된다.

## 이벤트 위임

이벤트 위임은 여러 하위 DOM 요소에 각각 이벤트 핸들러를 등록하는 대신 하나의 상위 DOM 요소에 이벤트 핸들러를 등록하는 방법

상위 요소에 이벤트 핸들러를 등록하기 때문에 이벤트 타깃이 개발자가 기대한 DOM 요소가 아닐 수 있다.

`Element.prototype.matches`

target ≠ currentTarget

## DOM 요소의 기본 동작 조작

### DOM 요소의 기본 동작 중단

preventDefault()

### 이벤트 전파 방지

stopPropagation

## 이벤트 핸들러 내부의 this

### 이벤트 핸들러 어트리뷰트 방식

this : window

### 이벤트 핸들러 프로퍼티 방식과 addEventListener 방식

this : 이벤트를 바인딩한 DOM 요소 (currentTarget)

화살표 함수 this : 상위 스코프의 this

클래스에서 이벤트 핸들러를 바인딩하면 this는 currentTarget을 가리킨다는 것에 주의하자.

⇒ bind, 화살표 함수를 사용할 수 있다.

## 이벤트 핸들러에 인수 전달

이벤트 핸들러 내부에서 함수를 호출하며 인수를 전달하거나

이벤트 핸들러를 반환하는 함수를 호출하며 인수를 전달할 수 있다.

## 커스텀 이벤트

### 커스텀 이벤트 생성

이벤트 생성자 함수를 호출해 명시적으로 생성한 이벤트 객체는 임의의 이벤트 타입을 지정할 수 있다.

이벤트 생성자 함수(이벤트 타입)

새로운 이벤트 타입을 지정할 경우 일반적으로 new CustomEvent(이벤트타입, detail프로퍼티)를 사용한다.

생성된 커스텀 이벤트 객체는 버블링되지 않으며 preventDefault로 취소할 수 없다.

bubbles와 cancelable 프로퍼티 값이 기본 false

커스텀 이벤트 객체의 bubbles, cancelable을 true로 설정하려면 두번째 인수로 이를 갖는 객체를 전달한다.

> 두번째 인수로 고유의 프로퍼티 값들을 전달한다.

커스텀 이벤트는 isTrusted 값이 언제나 false다.

### 커스텀 이벤트 디스패치

생성된 커스텀 이벤트는 dispatchEvent 메서드로 디스패치(이벤트를 발생시키는 행위)할 수 있다.

dispatchEvent 메서드에 이벤트 객체를 인수로 전달하면서 호출하면 인수로 전달한 이벤트 타입의 이벤트가 발생한다.

일반적으로 이벤트 핸들러는 비동기처리 방식으로 동작하지만 dispatchEvent 메서드는 이벤트 핸들러를 동기 처리 방식으로 호출한다.

dispatchEvent 메서드를 호출하면 커스텀 이벤트에 바인딩된 이벤트 핸들러를 직접 호출하는 것과 같다.

dispatchEvent 메서드로 이벤트를 디스패치하기 이전에 커스텀 이벤트를 처리할 이벤트 핸들러를 등록해야 한다.

이벤트 핸들러 어트리뷰트/프로퍼티를 사용할 수 없는 이유는 on이벤트타입 이벤트 핸들러 어트리뷰트/프로퍼티가 요소 노드에 존재하지 않기 때문이다.
