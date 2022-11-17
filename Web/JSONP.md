#JSONP

<aside>
💡 JSON with Padding

</aside>

## 동작 원리

웹 브라우저에서 실행되는 JavaScript는 동일 출처 정책에 따라 XMLHttpRequest 등의 직접적인 HTTP 통신을 이용해 외부 출처에서 데이터를 받아오는 것이 불가능하지만, HTML `<script>` 요소는 외부 출처로부터 조회된 내용을 실행하는 것이 허용되어 있다.

```html
<script src=”https://test.com”></script>
```

- 조건
  1. 서버에서 JSON형태로 데이터를 준다.
  2. script 태그로 받아온 JSON 데이터를 브라우저 어딘가에 저장해놓아야 한다.

## 사용 방법

```jsx
const script = document.createElement('script');
script.src = '//test.com/jsonp?callback=cb';

document.getElementsByTagName('head')[0].appendChild(script);

function cb(data) {
  //callback method
}
```
