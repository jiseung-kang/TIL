# 웹 컴포넌트

## 컴포넌트 아키텍처

<aside>
💡 일반적으로 컴포넌트는 기능과 페이지의 상호 작용 방식으로 설명할 수 있는 별도의 시각적 개체를 말한다.

</aside>

- 컴포넌트는 다음을 갖춰야 한다.

  - 고유한 자바스크립트 클래스
  - 외부코드가 접근할 수 없으며 해당 클래스에서만 관리되는 DOM 구조 (캡슐화 원칙)
  - 구성요소에 적용되는 CSS 스타일
  - 다른 구성요소와 상호작용하기 위한 이벤트, 클래스, 메서드 등을 일컫는 API

- 컴포넌트를 구축하기 위한 여러 프레임워크와 개발 방법론
  - 일반적으로 CSS 범위 지정, DOM 캡슐화 등을 제공하기 위한
  - 각자의 `CSS 클래스 및 규칙`들이 사용된다.

## 웹 컴포넌트

<aside>
💡 `CSS 클래스 및 규칙`을 위해 **내장된 브라우저 기능**을 제공한다.

</aside>

1. Custom elements

   사용자 정의 HTML 요소를 정의하는 데 사용된다.

2. Shadow DOM

   다른 컴포넌트에 숨겨져 있는 내부 DOM을 생성하는데 사용된다.

3. CSS Scoping

   컴포넌트의 Shadow DOM 내부에만 적용되는 스타일을 선언하는 데 사용된다.

4. Event retargeting

   사용자 정의 컴포넌트를 개발 환경에 더욱 적합하게 만든다.

## Custom elements

<aside>
💡 자체 메서드, 속성, 이벤트 등을 사용해 클래스에서 설명하는 사용자 지정 HTML 요소를 만들 수 있다.

</aside>

1. 자율 사용자 요소

   `HTMLElement` 추상 클래스를 확장하는 모든 새로운 요소

2. 사용자 빌트인 요소

   `HTMLButtonElement`를 기반한 사용자 버튼 등의 빌트인 요소를 확장한 요소

### Autonomous custom elements (자율적)

- 메서드로 다음을 브라우저에 알려줘야 한다.
  - 어떻게 보여줄 지
  - 요소가 추가되거나 제거될 때 무슨 일을 할지

```jsx
class MyElement extends HTMLElement {
  constructor() {
    super();
    // 요소가 생성될 때 단 한번 실행된다.
  }

  connectedCallback() {
    // 브라우저는 요소가 document에 추가되었을 때 이 메서드를 호출한다.
    // 여러번 실행될 수 있다.
  }

  disconnectedCallback() {
    // 브라우저는 요소가 document에서 제거될 때 이 메서드를 호출한다.
    // 여러번 실행될 수 있다.
  }

  static get observedAttributes() {
    return [
      /* 변경을 감지할 attribute들의 배열 */
    ];
  }

  attributeChangedCallback(name, oldValue, newValue) {
    // attribute 배열중 하나가 변경되었을 때 호출된다.
  }

  adoptedCallback() {
    // 요소가 다른 document로 이동될 때 실행된다.
    // document.adoptNode
  }

  // 그 외 여러 메서드 및 프로퍼티가 추가될 수 있다.
}

// 위 클래스로 만들 요소를 등록한다.
// MyElement의 인스턴스 <my-element>. 무조건 케밥 케이스!
customElements.define('my-element', MyElement);
// 이제 이렇게 쓸 수 있다.
document.createElement('my-element');
```

### Customized built-in elements (맞춤형)

- 위 같은 요소는 검색 엔진이나 웹 접근성에 대한 의미가 없다.
  - 내장 HTML 요소를 확장하고 사용자 정의해보자

```jsx
<script>
// The button that says "hello" on click
class HelloButton extends HTMLButtonElement {
  constructor() {
    super();
    this.addEventListener('click', () => alert("Hello!"));
  }
}

customElements.define('hello-button', HelloButton, {extends: 'button'});
</script>

<button is="hello-button">Click me</button>

<button is="hello-button" disabled>Disabled</button>
```
