# Tagged Template

<aside>
π‘ νκ·Έκ° μ§μ λ ννλ¦Ώ λ¦¬ν°λ΄μ ES6μ μλ‘μ΄ κΈ°λ₯μ΄λ€. 
ννλ¦Ώ λ¦¬ν°λ΄μ λ°μ λ ν ννλ‘ νκ·Έλ₯Ό μ¬μ©ν΄ ννλ¦Ώ λ¦¬ν°λ΄μ ν¨μλ‘ νμ±ν  μ μλ€.
</aside>

- λ³΄κ°λ²(`${}`)μ μ λ¬νμ§ μμΌλ©΄ μ²« λ²μ§Έ μΈμλ λ¬Έμμ΄μ΄ ν¬ν¨λ λ°°μ΄μ΄λ€.

```jsx
// λ€μμ λμΌνλ€.
fn`λ¬Έμμ΄`;
fn(['λ¬Έμμ΄']);
```

- λ³΄κ°λ²(`${}`)μ μ λ¬νλ©΄ λλ¨Έμ§ μΈμμ λ΄κΈ΄λ€.

```jsx
const aVar = 'λ³μ';

// λ€μμ λμΌνλ€.
fn` μλ ${aVar} μ§μΉ`;
fn(['μλ ', ' μ§μΉ'], aVar);
```

β ν¨μλ μ‘°μλ λ¬Έμμ΄μ λ°νν  μ μλ€.

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

λ€μμ μ¬μ©νλ©΄ escape sequence μ²λ¦¬ μμ΄ λ¬Έμμ΄μ μλ ₯ν λλ‘ μ κ·Όν  μ μλ€.

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
