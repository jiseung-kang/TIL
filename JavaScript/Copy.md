# 얕은 복사, 깊은 복사

## 자바스크립트의 얕은 복사와 깊은 복사\*\*

자바스크립트의 데이터 타입은 크게 객체 타입, 원시 타입으로 구분할 수 있다.

원시 타입은 숫자, 문자열, 불리언 등을 포함하며 변수에 할당하면 ‘실제 값 그대로' 저장된다. 그리고 다른 변수에 복사하면 원본의 원시 값이 그대로 복사되어 전달된다.

반면 객체 타입은 ‘참조에 의해' 저장되므로 변수에 할당하면 그 참조 값이 저장된다. 이 원본을 다른 변수에 할당하면 원본의 참조 값이 복사되어 전달된다.

이렇듯 자바스크립트의 객체 타입은 복사했을 때 동일 객체를 참조하는 현상이 나타날 수 있다. 그리고 우리는 이 현상에 대해, 동일 객체를 참조하는 복사의 형태를 얕은 복사, 동일한 객체를 참조하지 않고 완전히 독립된 복제본을 만드는 것을 깊은 복사라고 부른다.

[참조에 의한 전달](https://ko.javascript.info/object-copy)

## 자바스크립트의 얕은 복사와 깊은 복사의 방법\*\*

자바스크립트의 Array.prototype.concat(), Array.prototype.slice(), Array.from(), Object.assign()및 Object.create())은 깊은 복사본이 아닌 얕은 복사본을 만든다. 이러한 방법을 사용하면 원본 개체의 참조와 동일한 참조를 공유하며, 원본이나 복사본에 변경이 있으면 다른 개체도 함께 변경될 수 있다.

자바스크립트는 객체 복제 내장 메서드를 지원하지 않기 때문에 깊은 복제를 위해서는 새로운 객체를 만들고 원본 객체의 프로퍼티들을 순회하며 원시 수준까지 프로퍼티를 복사해야 한다.

JSON.parse(JSON.stringify())를 사용해 문자열로 직렬화 한 뒤 완전히 새로운 객체로 변환하는 방법이 있다. 이 경우 함수, Symbols 등 JSON.stringify()로 직렬화할 수 없는 것들에 대해 복사본을 만들 수 없다는 단점이 있다.

비슷하게 structureClone()를 사용하는 경우 Structured cloning algorithm을 사용해 보다 나은 성능을 보일 수 있지만, 이 역시 JSON.stringify()으로 직렬화할 수 없는 객체를 복제할 수 없으며, 자바스크립트 언어 자체의 기능이 아니라 아직은 브라우저 환경에서만 제공되는 메서드다.

완전한 깊은 복사를 위해서는 Structured cloning algorithm을 직접 구현해 재귀적으로 중첩된 객체를 복제하거나 lodash의 cloneDeep등을 사용해 깊은 복사를 처리해야만 한다.

[자바스크립트의 얕은 복사](https://developer.mozilla.org/en-US/docs/Glossary/Shallow_copy)

[자바스크립트의 깊은 복사](https://developer.mozilla.org/en-US/docs/Glossary/Deep_copy)

[참조에 의한 전달](https://ko.javascript.info/object-copy)
