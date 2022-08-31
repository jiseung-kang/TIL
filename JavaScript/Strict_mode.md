# Strict mode

## strict mode

암묵적 전역 등은 오류의 원인

이를 지원하기 위해 ES5부터 strict mode가 추가되었다.

자바스크립트 엔진의 최적화 작업에 문제를 일으킬 수 있는 코드에 대해 명시적인 에러를 발생시킨다.

ESLint 등으로도 유사한 효과를 얻을 수 있다.

> ES6에서 도입된 클래스와 모듈은 기본적으로 strict mode가 적용된다.

## strict mode의 적용

```jsx
"use strict";
```

## 전역에 strict mode 적용은 피하자

전역에 적용한 strict mode는 스크립트 단위로 적용된다.

외부 서드파티 라이브러리를 사용하는 경우 라이브러리가 non-strict mode일 가능성

즉시 실행 함수로 스크립트 전체를 감싸 스코프를 구분하고 strict mode를 적용하자

## 함수 단위로 strict mode를 적용하는 것도 피하자

섞어 쓰는 것에서 문제가 발생할 가능성

strict mode는 즉시 실행 함수로 감싼 스크립트 단위로 적용하는 것이 바람직

## strict mode가 잡아주는 에러

1. 암묵적 전역
   1. 선언하지 않은 변수 Reference Error
2. 변수, 함수, 매개변수의 삭제
   1. delete 연산자로 삭제시 SyntaxError
3. 매개변수 이름의 중복
   1. 중복된 매개변수 이름 SyntaxError
4. with문의 사용
   1. 전달된 객체를 스코프 체인에 추가한다.
   2. 객체 이름을 생략할 수 있어 코드가 간단해지지만
   3. 성능과 가독성에 안좋다.

## strict mode 적용에 의한 변화

1. 일반 함수의 this
   1. this에 undefined를 바인딩한다.
   2. 생성자 함수만 this가 필요하기 때문
2. arguments 객체
   1. 인수를 재할당해도 arguments 객체에 반영되지 않는다.
