#JSONP

<aside>
๐ก JSON with Padding

</aside>

## ๋์ ์๋ฆฌ

์น ๋ธ๋ผ์ฐ์ ์์ ์คํ๋๋ JavaScript๋ ๋์ผ ์ถ์ฒ ์ ์ฑ์ ๋ฐ๋ผ XMLHttpRequest ๋ฑ์ ์ง์ ์ ์ธ HTTP ํต์ ์ ์ด์ฉํด ์ธ๋ถ ์ถ์ฒ์์ ๋ฐ์ดํฐ๋ฅผ ๋ฐ์์ค๋ ๊ฒ์ด ๋ถ๊ฐ๋ฅํ์ง๋ง, HTMLย `<script>`ย ์์๋ ์ธ๋ถ ์ถ์ฒ๋ก๋ถํฐ ์กฐํ๋ ๋ด์ฉ์ ์คํํ๋ ๊ฒ์ด ํ์ฉ๋์ด ์๋ค.

```html
<script src=โhttps://test.comโ></script>
```

- ์กฐ๊ฑด
  1. ์๋ฒ์์ JSONํํ๋ก ๋ฐ์ดํฐ๋ฅผ ์ค๋ค.
  2. script ํ๊ทธ๋ก ๋ฐ์์จ JSON ๋ฐ์ดํฐ๋ฅผ ๋ธ๋ผ์ฐ์  ์ด๋๊ฐ์ ์ ์ฅํด๋์์ผ ํ๋ค.

## ์ฌ์ฉ ๋ฐฉ๋ฒ

```jsx
const script = document.createElement('script');
script.src = '//test.com/jsonp?callback=cb';

document.getElementsByTagName('head')[0].appendChild(script);

function cb(data) {
  //callback method
}
```
