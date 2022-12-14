# Shadow DOM

<aside>
π‘ Shadow DOMμ μΊ‘μν μ­ν μ νλ€. μ΄λ₯Ό ν΅ν΄ κ΅¬μ± μμ(μ»΄ν¬λνΈ)λ κ·Έλ§μ λ‘μ»¬ μ€νμΌ κ·μΉ λ±μ κ°μ§ μ μλ κ³ μ ν Shadow DOM Treeλ₯Ό κ°μ§ μ μλ€.

</aside>

## Built-in Shadow DOM

κ°λ°μ λκ΅¬λ₯Ό μ΄μμ λ `#shadow-root`μ λ³΄μ΄λ κ²μ `shadow DOM`μ΄λΌκ³  νλ€.

μΌλ°μ μΈ JavaScript νΈμΆμ΄λ μ νμλ‘ λ΄μ₯λ shadow DOMμ μ»μ μ μλ€.

μ΄λ μμ£Ό κ°λ ₯ν μΊ‘μν κΈ°μ μ΄λ€.

## Shadow Tree

- DOM μμλ λ κ°μ§ μ νμ νμ νΈλ¦¬κ° μλ€.
  - light tree
    - HTML μμμΌλ‘ κ΅¬μ±λ μΌλ° DOM νμ νΈλ¦¬
  - shadow tree
    - HTMLμ λ°μ¬μ€λμ§ μμ μ¨κ²¨μ§ DOM νμ νΈλ¦¬
- μμμ λ λ€ μμΌλ©΄ λΈλΌμ°μ λ shadow treeλ§ λ λλ§ νλ€.
  - κ΅¬μ±μ μ€μ ν  μ μλ€.
- shadow treeλ κ΅¬μ± μμ λ΄λΆλ₯Ό μ¨κΈ°κ³ , κ΅¬μ± μμ λ‘μ»¬ μ€νμΌμ μ μ©νκΈ° μν΄ μ¬μ©μ μ μ μμμμ μ¬μ©ν  μ μλ€.

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

shadow treeλ λ€μκ³Ό κ°μ νΉμ§μ΄ μλ€.

1. μμλΉ νλμ shadow rootλ₯Ό λ§λ€ μ μλ€.
2. λ°λμ μ¬μ©μ μμ λ§μ΄ shadow treeλ₯Ό κ΅¬μ±ν  μ μλ€.
3. μΊ‘μν μμ€μ λκ°μ§λ€.
   1. open : elem.shadowRoot.host === elem. λͺ¨λ  μ½λλ shadow νΈλ¦¬μ μ‘μΈμ€ν  μ μλ€.
   2. closed : elem.shadowRoot === null. μ‘μΈμ€ λΆκ°λ₯νλ€.

### μΊ‘μν

- Shadow DOM μμλ light DOMμμ λ³Ό μ μλ€.
  - μΆ©λνμ§ μλλ€.
- Shadow DOMμλ κ³ μ ν μ€νμΌμνΈκ° μλ€.
  - μΈλΆ DOM μ€νμΌ κ·μΉμ΄ μ μ©λμ§ μλλ€.
- Shadow treeμμ μμλ₯Ό κ°μ Έμ€λ €λ©΄ querySelect ν΄μΌ νλ€.

## μ€νμΌλ§

`:host` μ νμ μ¬μ©ν΄ shadow hostλ₯Ό μ νν  μ μλ€.

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

`::slotted(selector)`λ μ¬λ‘― μμ μμ²΄λ₯Ό μ νν  μ μμ§λ§ μμ μμλ μ νν  μ μλ€.

### μ»¨νμ€νΈ

```jsx
<body class="dark-theme">
  <!--
    :host-context(.dark-theme) applies to custom-dialogs inside .dark-theme
  -->
  <custom-dialog>...</custom-dialog>
</body>
```

### μ¬μ©μ μ μ CSS μμ±

μ΄λ shadow DOMμ ν¬ν¨ν΄ λͺ¨λ  κ³³μμ λ³΄κ³  μ¬μ©ν  μ μλ€.
