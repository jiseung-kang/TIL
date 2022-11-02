# 템플릿 요소

<aside>
💡 기본 <template> 요소는 HTML 마크업 템플릿의 저장소 역할을 한다.

</aside>

```jsx
<template>
  <tr>
    <td>Contents</td>
  </tr>
</template>
```

```jsx
<template>
  <style>
    p { font-weight: bold; }
  </style>
  <script>
    alert("Hello");
  </script>
</template>
```

- 브라우저는 `<templete>` 콘텐츠를 document 외부로 간주한다.
    - 스타일이 적용되지 않으며, 스크립트가 실행되지 않는다.
    - 콘텐츠를 live가 된다.

## 템플릿 삽입

<aside>
💡 DocumentFragment 처럼 content 속성으로 사용된다.

</aside>

복제, 삽입 시 DocumentFragment처럼 자식이 대신 삽입된다.

```jsx
<template id="tmpl">
  <style> p { font-weight: bold; } </style>
  <p id="message"></p>
</template>

<div id="elem">Click me</div>

<script>
  elem.onclick = function() {
    elem.attachShadow({mode: 'open'});

    elem.shadowRoot.append(tmpl.content.cloneNode(true)); // (*)

    elem.shadowRoot.getElementById('message').innerHTML = "Hello from the shadows!";
  };
</script>

// 이렇게 된다.
<div id="elem">
  #shadow-root
    <style> p { font-weight: bold; } </style>
    <p id="message"></p>
</div>
```

# 슬롯

<aside>
💡 Shadow DOM의 <slot>으로 Shadow DOM의 지정된 위치에 Light DOM 요소를 표시할 수 있다.

</aside>

## 명명된 슬롯

```jsx
<script>
customElements.define('user-card', class extends HTMLElement {
  connectedCallback() {
    this.attachShadow({mode: 'open'});
    this.shadowRoot.innerHTML = `
      <div>Name:
        <slot name="username"></slot>
      </div>
      <div>Birthday:
        <slot name="birthday"></slot>
      </div>
    `;
  }
});
</script>

<user-card>
  <span slot="username">John Smith</span>
  <span slot="birthday">01.01.2001</span>
</user-card>
```

최상위 자식만 slot 속성을 가질 수 있으며 중첩되는 경우 무시된다.

## 대체 콘텐츠

슬롯 내부에 무언가를 넣으면 기본 콘텐츠가 된다.

## 기본 슬롯

이름이 없는 slot은 모든 비슬롯 노드를 가져온다.

## 슬롯 업데이트

브라우저는 슬롯을 모니터링하고, 슬롯 요소가 추가/제거될 때 렌더링을 업데이트한다.

## 슬롯 API

node.assignedSlot : 할당된 slot 요소를 반환한다.

slot.assignedNodes : 슬롯에 할당된 DOM 노드

slot.assignedElements : 슬롯에 할당된 DOM 요소

slotChange 이벤트 : 슬롯이 처음 채워질 때, 슬롯이 있는 최상위요소가 추가/제거/변경 될 때 트리거