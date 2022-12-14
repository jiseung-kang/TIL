# 실행 컨텍스트

다음을 이해해보자

1. 자바스크립트가 스코프를 기반으로 식별자 바인딩을 관리하는 방식과 호이스팅 이유
2. 클로저의 동작 방식
3. 태스크 큐와 함께 동작하는 이벤트 핸들러
4. 비동기 처리의 동작 방식

## 소스코드의 타입

ECMAScript의 사양은 소스코드를 4가지 타입으로 구분한다.

이 타입에 따라 실행 컨텍스트를 생성하는 과정과 관리 내용이 다르다.

1. 전역 코드
   1. 전역에 존재하는 소스코드. 전역의 함수, 클래스 등의 내부 코드 X
   2. 전역 코드는 전역 변수를 관리하기 위해 최상위 스코프인 전역 스코프를 생성해야 한다.
   3. var 키워드로 선언된 전역 변수와 함수 선언문으로 정의된 전역 함수를 전역 객체의 프로퍼티와 메서드로 바인딩하고 참조하기 위해 전역 객체와 연결되어야 한다.
   4. 전역 코드가 평가되면 전역 실행 컨텍스트가 생성된다.
2. 함수 코드
   1. 함수 내부에 존재하는 소스코드. 함수 내부의 중첩 함수, 클래스 등의 내부 코드 X
   2. 지역 스코프를 생성하고 지역 변수, 매개 변수, arguments 객체를 관리해야 한다.
   3. 생성한 지역 스코프를 전역 스코프에서 시작하는 스코프 체인의 일원으로 연결한다.
   4. 함수 코드가 평가되면 함수 실행 컨텍스트가 생성된다.
3. eval 코드
   1. 빌트인 전역함수 eval 함수에 인수로 전달되어 실행되는 소스코드
   2. strict mode에서 자신만의 독자적인 스코프를 생성한다.
   3. eval 코드가 평가되면 eval 실행 컨텍스트가 생성된다.
4. 모듈 코드
   1. 모듈 내부에 존재하는 소스코드. 모듈 내부의 함수, 클래스 등의 내부 코드 X
   2. 모듈별로 독립적인 모듈 스코프를 생성한다.
   3. 모듈 코드가 평가되면 모듈 실행 컨텍스트가 생성된다.

## 소스코드의 평가와 실행

자바스크립트 엔진은 소스코드의 평가와 실행 과정으로 나누어 소스코드를 처리한다.

소스코드 평가 : 실행 컨텍스트를 생성하고 선언문만 먼저 실행한다. 생성된 변수, 함수 식별자를 키로 실행 컨텍스트가 관리하는 스코프(렉시컬 환경의 환경 레코드)에 등록한다.

소스코드 실행 : 선언문을 제외한 소스코드가 순차적으로 실행된다.(런타임) 이때 필요한 정보(변수, 함수 참조)를 실행 컨텍스트가 관리하는 스코프를 검색해서 취득한다.

소스코드의 실행 결과는 다시 실행 컨텍스트가 관리하는 스코프에 등록된다.

## 실행 컨텍스트의 역할

1. 전역 코드 평가
   1. 전역 코드 평가 과정을 거치며 실행을 준비한다.
   2. 선언문만 먼저 실행하고
   3. 생성된 전역 변수와 전역 함수가 실행 컨텍스트가 관리하는 전역 스코프에 등록된다.
   4. var키워드로 선언된 전역 변수와 함수 선언문으로 정의된 전역 함수는 전역 객체의 프로퍼티와 메서드가 된다.
2. 전역 코드 실행
   1. 런타임이 시작되어 전역 코드가 순차적으로 실행되기 시작한다.
   2. 이때 전역 변수에 값이 할당되고 함수가 호출된다.
   3. 함수가 호출되면 실행을 일시 중단하고 코드 실행 순서를 변경해 함수 내부로 진입한다.
3. 함수 코드 평가
   1. 함수 내부로 진입하면 함수 코드 평가 과정을 먼저 거치며 함수 코드를 실행할 준비를 한다.
   2. 이때 매개변수와 지역 변수 선언문이 먼저 실행되고
   3. 생성된 매개변수와 지역 변수가 실행 컨텍스트가 관리하는 지역 스코프에 등록된다.
   4. 함수 내부에서 지역 변수처럼 사용할 수 있는 arguments 객체가 생성되어 지역 스코프에 등록되고 this바인딩도 결정된다.
4. 함수 코드 실행
   1. 런타임이 시작되어 함수 코드가 순차적으로 실행되기 시작한다.
   2. 매개변수와 지역 변수에 값이 할당된다.
   3. 식별자가 등장하면 스코프 체인을 통해 검색한다.
   4. 함수 코드의 지역 스코프는 상위 스코프인 전역 스코프와 연결되어야 한다.
   5. 식별자가 전역 객체에 프로퍼티로 존재할 수도 있다. 전역 객체의 프로퍼티는 마치 전역 변수처럼 전역 스코프를 통해 검색 가능해야 한다.
   6. 식별자를 찾으면 프로퍼티를 프로토타입 체인을 통해 찾고 평가된다.
   7. 실행이 종료되면 함수 코드 실행 과정이 종료되고 함수 호출 이전으로 되돌아가 전역 코드 실행을 계속한다.
      - 함수 호출 이전으로 되돌아가려면
      - 현재 실행 중인 코드와 이전에 실행하던 코드를 구분해서 관리해야 한다.
      - 이를 위해 다음과 같은 스코프, 식별자, 코드 실행 순서 등의 관리가 필요하다.
        - 선언에 의해 생성된 모든 식별자를 스코프를 구분해 등록하고 상태 변화를 지속적으로 관리해야 함
        - 스코프는 중첩 관계에 의해 스코프 체인을 형성해야 한다.
        - 현재 실행 중인 코드의 실행 순서를 변경하고 다시 되돌아갈 수도 있어야 한다.
      - 이것들을 관리하는게 바로 실행 컨텍스트

> 실행 컨텍스트는 소스코드를 실행하는 데 필요한 환경을 제공하고 코드의 실행 결과를 실제로 관리하는 영역이다.
> 실행 컨텍스트는 식별자를 등록하고 관리하는 스코프와 코드 실행 순서 관리를 구현한 내부 메커니즘
> 모든 코드는 실행 컨텍스트를 통해 실행되고 관리된다.
> 식별자와 스코프는 실행 컨텍스트의 렉시컬 환경으로 관리하고
> 코드 실행 순서는 실행 컨텍스트 스택으로 관리한다.

## 실행 컨텍스트 스택

실행 컨텍스트는 스택 자료구조로 관리된다.

1. 전역 코드의 평가와 실행
   1. 먼저 전역 코드를 평가하고 전역 실행 컨텍스트를 생성하고 실행 컨텍스트 스택에 푸시
   2. 전역 변수, 전역 함수 등은 전역 실행 컨텍스트에 등록된다.
   3. 전역 코드가 실행되기 시작해서 전역 변수에 값이 할당되고 전역 함수가 호출된다.
2. 전역 함수 코드의 평가와 실행
   1. 전역 함수가 호출되면 전역 코드의 실행이 일시 중단되고 코드의 제어권이 함수 내부로 이동한다.
   2. 자바스크립트 엔진은 함수 내부의 함수 코드를 평가해 함수 실행 컨텍스트를 생성하고 실행 컨텍스트 스택에 푸시한다.
   3. 지역변수와 중첩 함수가 전역 함수의 실행 컨텍스트에 등록된다.
   4. 전역 함수 코드가 실행되기 시작하고 지역 변수에 값이 할당되고 중첩 함수가 호출된다.
3. 중첩 함수 코드의 평가와 실행
   1. 전역 함수 코드의 실행이 일시 중단되고 코드의 제어권이 함수 내부로 이동한다.
   2. 자바스크립트 엔진은 함수 내부의 함수 코드를 평가해 중첩 함수 실행 컨텍스트를 생성하고 실행 컨텍스트 스택에 푸시한다.
   3. 중첩함수의 지역변수가 중첩함수의 실행 컨텍스트에 등록된다.
   4. 중첩 함수 코드가 실행되기 시작하고 지역 변수에 값이 할당되고 종료된다.
4. 전역 함수 코드로 복쉬
   1. 중첩 함수가 종료되면 코드의 제어권은 다시 전역 함수로 이동한다.
   2. 자바스크립트 엔진은 중첩 함수의 실행 컨텍스트를 실행 컨텍스트 스택에서 팝하여 제거한다.
   3. 전역 함수는 종료된다.
5. 전역 코드로 복귀
   1. 전역 함수가 종료되면 코드의 제어권은 다시 전역 코드로 이동한다.
   2. 자바스크립트 엔진은 전역 함수 실행 컨텍스트를 실행 컨텍스트 스택에서 팝하여 제거한다.
   3. 전역 실행 컨텍스트도 실행 컨텍스트 스택에서 팝되어 실행 컨텍스트 스택에는 아무것도 안 남는다.

> 실행 컨텍스트 스택은 코드의 실행 순서를 관리한다.
> 실행 컨텍스트 스택의 최상위에 존재하는 실행 컨텍스트는 언제나 현재 실행 중인 코드의 실행 컨텍스트다.
> 이것을 실행 중인 실행 컨텍스트라고 부른다.

## 렉시컬 환경

> 렉시컬 환경은 식별자와 식별자에 바인딩된 값, 상위 스코프에 대한 참조를 기록하는 자료구조로 실행 컨텍스트를 구성하는 컴포넌트다.

실행 컨텍스트 스택 : 코드의 실행 순서를 관리

렉시컬 환경: 스코프와 식별자를 관리

렉시컬 환경은 키와 값을 갖는 객체 형태의 스코프를 생성해 식별자를 키로 등록하고 식별자에 바인딩된 값을 관리한다.

> 렉시컬 환경 : 스코프를 구분하여 식별자를 등록하고 관리하는 저장소역할을 하는 렉시컬 스코프의 실체

실행 컨텍스트 : LexicalEnvironment 컴포넌트, VariableEncironment 컴포넌트

- 생성 초기에 LexicalEnvironment 컴포넌트와 VariableEnvironment 컴포넌트는 하나의 동일한 렉시컬 환경을 참조한다.
- 특수한 상황에서 VariableEnvironment 컴포넌트를 위한 새로운 렉시컬 환경이 생성되고 둘의 내용이 달라지기도 한다.

**렉시컬 환경**

1. 환경 레코드
   1. 스코프에 포함된 식별자를 등록하고 등록된 식별자에 바인딩된 값을 관리하는 저장소
   2. 환경 레코드는 소스코드의 타입에 따라 관리하는 내용에 차이가 있다.
2. 외부 렉시컬 환경에 대한 참조
   1. 상위 스코프 : 해당 실행 컨텍스트를 생성한 소스코드를 포함하는 상위 코드의 렉시컬 환경
   2. 이것을 통해 단방향 링크드 리스트인 스코프 체인을 구현한다.

## 실행 컨텍스트의 생성과 식별자 검색 과정

1. 전역 객체 생성
   1. 전역 코드가 평가되기 이전에 생성된다.
   2. 빌트인 전역 프로퍼티, 빌트인 전역 함수, 표준 빌트인 객체가 추가되어 동작 환경에 따라 클라이언트 사이트 Web API 또는 특정 환경을 위한 호스트 객체를 포함한다.
   3. 전역 객체도 Object.prototype을 상속받는다. (프로토타입 체인의 일원)
2. 전역 코드 평가
   1. 전역 실행 컨텍스트 생성
      1. 비어있는 전역 실행 컨텍스트를 생성해서 실행 컨텍스트 스택에 푸시
   2. 전역 렉시컬 환경 생성, 전역 실행 컨텍스트에 바인딩

      전역 환경 레코드 생성 : ES6 이전에는 전역 객체가 전역 환경 레코드 역할을 수행했지만 이제는 전역 변수가(var 제외) 개념적인 블록 내에 존재한다. 객체 환경 레코드와 선언적 환경 레코드는 협력해서 전역 스코프와 전역 객체를 관리한다.

      1. 객체 환경 레코드 생성
         1. 기존 전역 객체가 var 키워드로 선언한 전역 변수, 함수 선언문으로 정의한 전역 함수, 빌트인 전역 프로퍼티, 빌트인 전역 함수, 표준 빌트인 객체 관리
         2. 이때 등록된 식별자를 전역 환경 레코드의 객체 환경 레코드에서 검색하면 전역 객체의 프로퍼티를 검색해 반환한다.
         3. 이게 전역 객체 식별자 없이 전역 객체의 프로퍼티를 참조할 수 있는 메커니즘
         4. 객체 환경 레코드는 전역 객체와 연결된다.
         5. 호이스팅의 원인이 되는 메커니즘
      2. 선언적 환경 레코드 생성
         1. let, const 키워드로 선언한 전역 변수 관리
         2. 그 개념적인 블록이 바로 여기

   3. this 바인딩
      1. this 바인딩은 전역 환경 레코드와 함수 환경 레코드에만 존재한다.
      2. 전역 환경 레코드의 [[GlobalThisValue]] 내부 슬롯에 this가 바인딩된다.
      3. 일반적으로 전역 객체가 바인딩된다.
      4. 전역 코드에서 this를 참조하면 전역 환경 레코드의 [[GlobalThisValue]] 내부 슬롯에 바인딩되어 있는 객체가 반환된다.
   4. 외부 렉시컬 환경에 대한 참조 결정
      1. 현재 평가 중인 소스코드를 포함하는 외부 소스코드의 렉시컬 환경, 즉 상위 스코프를 가리킨다. 이를 통해 단방향 링크드인 리스트 스코프 체인을 구현한다.
3. 전역 코드 실행

   전역 코드가 순차적으로 실행되기 시작한다.

   식별자 결정 : 어느 스코프의 식별자를 참조할지 결정한다.

   실행 중인 실행 컨텍스트의 렉시컬 환경에서 식별자를 검색할 수 없으면 외부 렉시컬 환경에 대한 참조가 가리키는 렉시컬 환경, 즉 상위 스코프로 이동하여 식별자를 검색한다.

4. 함수 코드 평가
   1. 함수 실행 컨텍스트 생성
      1. 함수 렉시컬 환경이 완성된 다음 실행 컨텍스트에 푸시된다.
   2. 함수 렉시컬 환경 생성
      1. 렉시컬 환경을 생성하고 나서 a의 실행 컨텍스트에 바인딩된다.
      2. 렉시컬 환경은 환경 레코드와 외부 렉시컬 환경에 대한 참조
         1. 함수 환경 레코드 생성 : 매개변수, arguments 객체, 지역 변수와 중첩 함수 등록 관리
         2. this 바인딩 : 함수 호출 방식에 따라 this 바인딩
         3. 외부 렉시컬 환경에 대한 참조 결정 : 실행 중인 실행 컨텍스트의 렉시컬 환경의 참조 할당
      3. 자바스크립트 엔진은 함수 정의를 평가해 함수 객체를 생성할 때 현재 실행 중인 실행 컨텍스트의 렉시컬 환경, 즉 함수의 상위 스코프를 함수 객체의 내부 슬롯 [[Environment]]에 저장한다. 함수 렉시컬 환경의 내부 슬롯 [[Environment]]에 저장된 렉시컬 환경의 참조
5. 함수 코드 실행
   1. 순차적으로 실행
   2. 식별자 결정을 위해 실행중인 실행 컨텍스트의 렉시컬 환경에서 식별자를 검색하기 시작한다.
   3. 검색된 식별자에 값을 바인딩
6. 중첩 함수 코드 평가
   1. 함수 내부로 코드 제어권이 이동한다.
7. 중첩 함수 코드 실행
   1. 런타임이 시작되어 함수의 소스코드 순차 실행
8. 중첩 함수 코드 실행 종료
   1. 실행 컨텍스트 스택에서 중첩 함수 실행 컨텍스트 팝
   2. 렉시컬 환경은 독립적인 객체
   3. 가비지 컬렉터에 의해 나중에 제거된다.
9. 함수 코드 실행 종료
   1. 함수 실행 컨텍스트 팝되어 제거
10. 전역 코드 실행 종료
    1. 전역 실행 컨텍스트도 팝된다.

## 실행 컨텍스트와 블록 레벨 스코프

블록 레벨 스코프를 위해 선억적 환경 레코드를 갖는 렉시컬 환경을 새롭게 생성해 기존의 전역 렉시컬 환경을 교체한다.

새로운 블록을 위한 렉시컬 환경의 외부 렉시컬 환경에 대한 참조는 블록문 실행 이전의 렉시컬 환경을 가리킨다.
