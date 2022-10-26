# 커링(Currying)

<aside>
💡 함수와 함께 사용할 수 있는 고급 기술. 여러 언어에 존재한다.

</aside>

- 커링은
  - `f(a, b, c)` 같은 단일 호출 함수를
  - `f(a)(b)(c)` 처럼 각각의 인수가 호출 가능한 프로세스로 호출된 후 병합되도록 변환하는 것

## Usage

```jsx
function curry(f) {
  // 커링 변환을 하는 curry(f) 함수
  return function (a) {
    return function (b) {
      return f(a, b);
    };
  };
}

// usage
function sum(a, b) {
  return a + b;
}

let curriedSum = curry(sum);

alert(curriedSum(1)(2)); // 3
```

## 장점

- 커링을 적용하기 전과 후가 동일하게 동작한다.
- partial 함수를 편리하게 구현할 수 있다.
  - 함수형 프로그래밍에 유리하다.
  - 범용 함수를 정확한 인수의 개수로 호출할 수 있게 해준다.

## 특징

- 오직 고정된 길이의 함수들만 사용 가능하다.
  - rest 파라미터 등을 사용할 수 없다.
- 커링은 다중 인수에 대한 단일 프로세스 함수 호출을 다중 callable 프로세스 형태로 변형하는 것이다.
