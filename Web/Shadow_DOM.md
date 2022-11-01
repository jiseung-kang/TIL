# Shadow DOM

<aside>
💡 Shadow DOM은 캡슐화 역할을 한다. 이를 통해 구성 요소(컴포넌트)는 그만의 로컬 스타일 규칙 등을 가질 수 있는 고유한 Shadow DOM Tree를 가질 수 있다.

</aside>

## Built-in Shadow DOM

개발자 도구를 열었을 때 `#shadow-root`에 보이는 것을 `shadow DOM`이라고 한다.

일반적인 JavaScript 호출이나 선택자로 내장된 shadow DOM을 얻을 수 없다.

이는 아주 강력한 캡슐화 기술이다.

## Shadow Tree

- DOM 요소는 두 가지 유형의 하위 트리가 있다.
  - light tree
    - HTML 자식으로 구성된 일반 DOM 하위 트리
  - shadow tree
    - HTML에 반여오디지 않은 숨겨진 DOM 하위 트리
- 요소에 둘 다 있으면 브라우저는 shadow tree만 렌더링 한다.
  - 구성을 설정할 수 있다.
- shadow tree는 구성 요소 내부를 숨기고, 구성 요소 로컬 스타일을 적용하기 위해 사용자 정의 요소에서 사용할 수 있다.

```jsx
<script>
customElements.define('show-hello', class extends HTMLElement {
  connectedCallback() {
    const shadow = this.attachShadow({mode: 'open'});
    shadow.innerHTML = `<p>
      Hello, ${this.getAttribute('name')}
    </p>`;
  }
});
</script>

<show-hello name="John"></show-hello>
```

shadow tree는 다음과 같은 특징이 있다.

1. 요소당 하나의 shadow root를 만들 수 있다.
2. 반드시 사용자 요소 만이 shadow tree를 구성할 수 있다.
3. 캡슐화 수준은 두가지다.
   1. open : elem.shadowRoot.host === elem. 모든 코드는 shadow 트리에 액세스할 수 있다.
   2. closed : elem.shadowRoot === null. 액세스 불가능하다.

### 캡슐화

- Shadow DOM 요소는 light DOM에서 볼 수 없다.
  - 충돌하지 않는다.
- Shadow DOM에는 고유한 스타일시트가 있다.
  - 외부 DOM 스타일 규칙이 적용되지 않는다.
- Shadow tree에서 요소를 가져오려면 querySelect 해야 한다.

## 스타일링

`:host` 선택을 사용해 shadow host를 선택할 수 있다.

```jsx
<template id="tmpl">
  <style>
    /* the style will be applied from inside to the custom-dialog element */
    :host {
      position: fixed;
      left: 50%;
      top: 50%;
      transform: translate(-50%, -50%);
      display: inline-block;
      border: 1px solid red;
      padding: 10px;
    }

		custom-dialog {
		  padding: 0;
		}
  </style>
  <slot></slot>
</template>

<script>
customElements.define('custom-dialog', class extends HTMLElement {
  connectedCallback() {
    this.attachShadow({mode: 'open'}).append(tmpl.content.cloneNode(true));
  }
});
</script>

<custom-dialog>
  Hello!
</custom-dialog>
```

`::slotted(selector)`는 슬롯 요소 자체를 선택할 수 있지만 자식 요소는 선택할 수 없다.

### 컨텍스트

```jsx
<body class="dark-theme">
  <!--
    :host-context(.dark-theme) applies to custom-dialogs inside .dark-theme
  -->
  <custom-dialog>...</custom-dialog>
</body>
```

### 사용자 정의 CSS 속성

이는 shadow DOM을 포함해 모든 곳에서 보고 사용할 수 있다.
