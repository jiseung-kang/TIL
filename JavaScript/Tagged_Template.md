# Tagged Template

<aside>
💡 태그가 지정된 템플릿 리터럴은 ES6의 새로운 기능이다. 
템플릿 리터럴의 발전된 한 형태로 태그를 사용해 템플릿 리터럴을 함수로 파싱할 수 있다.
</aside>

- 보간법(`${}`)을 전달하지 않으면 첫 번째 인수는 문자열이 포함된 배열이다.

```jsx
// 다음은 동일하다.
fn`문자열`;
fn(['문자열']);
```

- 보간법(`${}`)을 전달하면 나머지 인수에 담긴다.

```jsx
const aVar = '변수';

// 다음은 동일하다.
fn` 안녕 ${aVar} 지승`;
fn(['안녕 ', ' 지승'], aVar);
```

⇒ 함수는 조작된 문자열을 반환할 수 있다.

```jsx
const person = 'Mike';
const age = 28;

const myTag = (strings, personExp, ageExp) => {

  const str0 = strings[0]; // "that "
  const str1 = strings[1]; // " is a "

  const ageStr;
  if (ageExp > 99){
    ageStr = 'centenarian';
  } else {
    ageStr = 'youngster';
  }

  return str0 + personExp + str1 + ageStr;

}

const output = myTag`that ${ person } is a ${ age }`;

console.log(output);
// that Mike is a youngster
```

## Raw strings

다음을 사용하면 escape sequence 처리 없이 문자열을 입력한 대로 접근할 수 있다.

```jsx
const tag = (strings) => {
  console.log(strings.raw[0]);
};

tag`string text line 1 \n string text line 2`;
// string text line 1 \n string text line 2
```

## ES2018 escape sequence

```jsx
const latex = (str) => {
  return { cooked: str[0], raw: str.raw[0] };
};

latex`\unicode`;
// { cooked: undefined, raw: "\\unicode" }
```
