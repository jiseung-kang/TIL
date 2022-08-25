# Symbol

## Symbol

다른 값과 중복되지 않는 유일무이한 값

프로퍼티 키로 사용할 수 있다.

## Symbol 생성하기

Symbol 함수를 호출하면 외부로 노출되지 않는 유일무이한 값이 생성된다.

new 없이 호출하는 변경 불가능한 원시 값이다.

선택적으로 문자열을 전달할 수 있지만, 디버깅 용도로만 쓰인다.

객체처럼 접근하면 암묵적으로 래퍼 객체를 생성한다.

```jsx
symbol.description;
symbol.toString();
```

암묵적으로 문자열이나 숫자 타입으로 변환되지 않는다. // TypeError

## Symbol.for / Symbol.keyFor

- Symbol.for
  - 인수로 전달받은 문자열을 키로 키와 심벌 값 쌍들이 저장된 전역 심벌 레지스트리에서 해당 키와 일치하는 심벌 값을 검색한다.
    - 있으면 반환한다.
    - 없으면 생성해서 저장한다.
- Symbol.keyFor
  - 전역 심벌 레지스트리에 저장된 심벌 값의 키를 추출할 수 있다.

## 심벌과 상수

특별한 의미 없이 상수 이름 자체에 의미가 있는 경우 심벌 값을 사용할 수 있다.

- enum
  Object.freeze 메서드와 심벌 값을 사용해 enum을 흉내낼 수 있다.

## 심벌과 프로퍼티 키

객체의 프로퍼티 키는 빈 문자열을 포함하는 모든 문자열 또는 심벌 값

심벌 값을 프로퍼티 키로 사용하려면 대괄호를 사용해야 한다.

## 심벌과 프로퍼티 은닉

심벌 값을 프로퍼티 키로 사용하면 for … in 문, Object.keys, Object.getOwnPropertyNames 메서드로 찾을 수 없다.

하지만 완전한 은닉은 아니다. (Object.getOwnPropertySymbols)

## 심벌과 표준 빌트인 객체 확장

표준 빌트인 객체는 읽기 전용으로 사용하자. 이유는 중복의 위험성

중복될 가능성이 없는 심벌 값으로 프로퍼티 키를 생성해 표준 빌트인 객체를 확장하면 이 위험을 줄이면서 표준 빌트인 객체를 확장할 수 있다.

## Well-known Symbol

빌트인 심벌 값은 Symbol 함수의 프로퍼티에 할당되어 있다.

Array, String, Map, Set, TypeArray, arguments, NodeList, HTMLCollection과 같이 for … of로 순회 가능한 빌트인 이터러블은 Well-known Symbol인 Symbol.iterator를 키로 갖는 메서드를 가진다.

Symbol.iterator 메서드를 호출하면 이터레이터를 반환한다.

이런 식으로 Symbol.iterator를 메서드의 키로 하면 기존/미래의 프로퍼티와 중복되지 않을 것이다.

> 심벌은 중복되지 않는 상수 값을 생성하며,
> 기존에 작성된 코드에 영향을 주지 않고 새로운 프로퍼티를 추가하기 위해 도입되었다.
