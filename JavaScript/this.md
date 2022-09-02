# this

## this

객체 : 상태를 나타내는 프로퍼티와 동작을 나타내는 메서드를 하나의 논리적인 단위로 묶은 복합적인 자료구조

> 동작을 나타내는 메서드는 자신이 속한 객체의 상태, 즉 프로퍼티를 참조하고 변경할 수 있어야 한다.
> ⇒ **자신이 속한 객체를 가리키는 식별자를 참조할 수 있어야 한다.**

`this`는 **자신이 속한 객체** 또는 **자신이 생성할 인스턴스**를 가리키는 자기 참조 변수다.

`this`를 통해 자신이 속한 객체 또는 자신이 생성할 인스턴스의 프로퍼티나 메서드를 참조할 수 있다.

`this`는 자바스크립트 엔진에 의해 암묵적으로 생성되며, 코드 어디서든 참조할 수 있다.

함수를 호출하면 arguments 객체와 this가 암묵적으로 함수 내부에 전달된다.

> `this` 바인딩은 함수 호출 방식에 의해 동적으로 결정된다.
> 바인딩 : 식별자와 값을 연결하는 과정

- 일반 함수 내부에서 this는 전역 객체 window (strict mode에서는 undefined)
- 메서드 내부에서 this는 메서드를 호출한 객체
- 생성자 함수 내부에서 this는 생성자 함수가 생성할 인스턴스

## 함수 호출 방식과 this 바인딩

> 렉시컬 스코프와 this 바인딩은 결정 시기가 다르다.

1. 일반 함수 호출
   1. 기본적으로 this에는 전역 객체가 바인딩된다.
   2. 중첩 함수의 this도 마찬가지. 의미없다.
   3. strict mode에서 undefined
   4. 어떤 함수라도 일반 함수로 호출되면 전역 객체가 바인딩된다.
   5. Function.prototype.apply/call/bind 메서드를 사용해 명시적으로 바인딩해야 한다.
   6. 또는 화살표 함수를 사용해서 this 바인딩을 일치시켜야 한다.
   7. 화살표 함수 내부의 this는 상위 스코프의 this를 가리키기 때문이다.
2. 메서드 호출
   1. 마침표 연산자 앞에 기술한 객체가 바인딩된다.
3. 생성자 함수 호출
   1. 생성자 함수 내부의 this에는 생성자 함수가 생성할 인스턴스가 바인딩된다.
4. Function.prototype.apply/call/bind에 의한 간접 호출
   1. 첫번째 인수로 전달한 객체가 바인딩된다.
   2. 이들 메서드는 모든 함수가 상속받아 사용할 수 있다.

      ```jsx
      // this로 사용할 객체, 인수 리스트
      Function.prototype.apply(thisArg[, argsArray]) // 배열 또는 유사 배열 객체
      Function.prototype.call(thisArg[, arg1[, arg2[, ...]]) // 인수 리스트
      ```

   3. apply, call의 대표적인 용도는 유사 배열 객체에 배열 메서드를 사용하는 경우
   4. bind는 함수를 호출하지 않고 단순히 this 바인딩이 교체된 함수를 새롭게 생성해 반환한다.
   5. bind는 메서드의 this와 메서드 내부의 중첩 함수 또는 콜백 함수의 this가 불일치하는 문제를 해결한다.