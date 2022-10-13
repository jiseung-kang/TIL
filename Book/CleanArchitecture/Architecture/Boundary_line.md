# 경계 : 선 긋기

소프트웨어 아키텍처 = 선을 긋는 기술

선 = 경계

경계 = 소프트웨어 요소를 서로 분리하고 반대편을 알지 못하게 하는 것

아키텍처의 목표 = 시스템을 만들고 유지하는 인적 자원을 최소화하는 것

결합 = 인적 자원의 효율을 떨어뜨리는 것. 이른 결정의 결과

이른 결정 = 시스템의 업무 요구사항, 유스케이스와 관련 없는 결정 (프레임워크, 데이터베이스, 웹 서버, 유틸리티 라이브러리, 의존성 주입에 대한 결정)

### 두 가지 슬픈 이야기

- 웹이 대세가 되었다.
  - 웹 솔루션 필요
  - 이른 결정
  - 개발 비용 가중
- 소프트웨어 작업을 통제하자
  - 서비스 지향 아키텍처
  - 서비스 사이의 결합
  - SOA를 약속하는 도구들을 너무 일찍 채택 적용

### FitNesse

- 우리만의 웹 서버를 직접 작성하자
  - 웹 프레임워크 사용은 나중에 생각하자
  - 데이터베이스 고민하지 말자
  - 필요할 때가 되어서야 차례대로 수행
  - 필요하면 다시 한번 고민하고 결정
- 개발 초기에 업무 규칙과 데이터베이스 사이에 경계선을 그었다.
  - 업무 규칙은 데이터베이스에 대해 모른다.
  - 데이터베이스 구현 연기
  - 방향을 바꾸기 쉬움
- 결정은 늦추고 연기하는 건
  - 시간을 절약해준다

### 어떻게 선을 그을까, 언제 그을까?

선 = 관련이 있는 것과 없는 것 사이에 긋는 것

데이터베이스를 결정하기에 앞서 업무 규칙을 먼저 작성하고 테스트하는 데 집중하자

### 입력과 출력

시스템이 뭘까? 입출력은 중요하지 않다. 그것은 행위적인 측면

중요한 것은 업무 규칙

### 플러그인 아키텍처

- 소프트 웨어 기술의 역사
  - 플러그인을 손쉽게 생성해
  - 확장 가능하며
  - 유지보수가 쉬운
  - 시스템 아키텍처 확립에 대한 것
  - 선택적이거나 다양한 형태로 구현될 수 있는 나머지 컴포넌트로부터 핵심적인 업무 규칙은 분리되어 있고 독립적

### 플러그인에 대한 논의

- 특정 모듈은 나머지 모듈에 영향 받지 않아야
- 시스템을 플러그인 아키텍처로 배치해 변경이 전파될 수 없는 방화벽을 생성
- 경계는 변경의 축
- 결국 단일 책임 원칙

### 결론

시스템을 먼저 컴포넌트 단위로 분할하라

일부 컴포넌트는 핵심 업무 규칙

나머지 컴포넌트는 플러그인 : 필수 기능

그 다음 소스를 배치하자

⇒ 의존성 역전 원칙 + 안정된 추상화 원칙

⇒ 읜존성 화살표는 저수준 세부사항에서 고수준 추상화