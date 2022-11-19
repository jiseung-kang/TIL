tabindex : -1 포함 여부

# focusable

<aside>
💡 대화형 요소에는 tabindex=”0”을 추가해 포커스 가능하게 만들어야 한다.

</aside>

- 요소에 focus 하는 방법
  - element.focus()
  - tabindex=0

## tabindex=”0”

- 값이 0이면 요소가 HTML 문서의 요소 순서를 기반으로 하는 기본 포커스 순서의 일부임을 나타낸다.
- 양수 값을 사용하면 기본 순서의 요소보다 먼저 배치되므로 논리적으로 혼란스럽다.

## tabindex=”-1”

- 순차적 키보드 탐색으로 요소에 도달할 수 없다.
- JavaScript, 마우스 클릭으로 초점을 맞출 수 있다.

# Tabbable

- 선택하지 않은 요소
  - hidden
  - aria-selected=”false”
  - tabindex=”-1-
- 선택한 요소
  - hidden 제거
  - aria-selected=”true”
  - tabindex=”0”
