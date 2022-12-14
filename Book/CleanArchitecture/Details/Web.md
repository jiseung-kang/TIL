# 웹은 세부사항이다

1. 연산 능력이 모두 서버 팜에 위치할 것이다.
   1. 브라우저는 하는 일이 없을 것이다.
2. 브라우저에 애플릿 추가
3. 웹 2.0 고안
   1. Ajax, 자바스크립트를 이용해 처리 과정의 많은 부분을 다시 브라우저로 옮겼다.
4. 현재는 애플리케이션 전부를 브라우저에서 실행되도록 작성하는 수준
5. Node.js를 이용해 자바스크립트를 다시 서버로 이동시키는 중

## 끝없이 반복하는 추

그린 스크린 단말기 → 중앙집중식 미니컴퓨터 → 클라이언트-서버 아키텍처

- 그래서 연산 능력을 어디에 둘 것인가
  - 중앙 집중 vs 분산 방식
- 다 떠나서
  - 업무 규칙을 UI로부터 분리해야 한다.

## 요약

- GUI는 세부사항
  - 웹은 GUI
  - 세부사항은 핵심 업무 로직에서 분리해야 한다.
- 자바스크립트
  - 유효성 검증, 드래그앤드롭방식 Ajax 호출 등의 복잡함
  - 웹에서 장치 독립성은 비현식적?
  - 애플리케이션과 GUI의 상호작용이 빈번하긴 하다.
  - 업무 로직은 다수의 유스케이스로 구성
  - 완전한 입력 데이터와 그에 따른 출력 데이터를 데이터 구조로 만들어 유스케이스를 실행하는 처리 과정의 입력 값과 출력 값으로 사용할 수 있다.
  - 이렇게 하면 각 유스케이스가 장치 독립적인 방식으로 UI라는 입출력 장치를 동작시킨다고 할 수 있다.

## 결론

이러한 추상화를 제대로 하면 좋다.
