# Software Development Life Cycle(SDLC)

- 계획, 개발, 시험, 배포
- 요구사항 분석 → 설계 → 구현 → 테스트 → 유지보수

## 소프트웨어 공학

- ‘정량적’ 학문
- 버전 관리
- 프로젝트 관리

**manout** : 노동 시간 && 산출물

⇒ 여러가지 요소들을 정량적으로 판단, 측정

<aside>
💡 So , , , 우리는 프로젝트를 어떻게 관리해야 할까?

</aside>

## Models

### 👷‍♀️ build & fix

- 지금 하는거
- 기획, 설계, 유지보수 그런거 없다.

### 🧪 Prototype

- **최소한의 요구사항을 분석**하고 프로토타입을 제작

### 💧 Waterfall

- 요구사항 분석 설계 후 구현 (모두 다같이, 차례대로)
- 문제 상황 발생
- 요구사항 다시 분석, 다시 설계, 수정? 불가능
- serious하지 않다면 이전 단계로 돌아갈 수 없음
- 비합리적이나 이 기능 구현에 대한 side effect를 피하기 위함
- 프로젝트 관리가 쉬움
- 단계별 산출물이 뚜렷하다. (요구사항 분석 명세서, ERD … , 유스케이스, 디자인 프로토타입, 코드, 테스트 결과지, 로그…)
- Plan-Driven : 간트 차트

### 🌀 Spiral

- 목표설정 → 위험분석 → 개발, 검증 → 고객평가, 다음 단계 수립을 반복
- cycle에 의해 진전이 안되는 듯 보이나, core에 가까울수록 안정도가 높다.
- 위험을 최소화할 수 있음
- 안정성을 추구하는 대형 시스템 (금융)
- 시간, 비용이 비효율적

### ➰ Agile Software development

- 프로젝트의 생명주기 동안 작은 단위의 반복적인 개발
- TMP(Too Much Plan) X TLP(Too Less Plan) 절충
- Code-Oriented Methodology
- 프레임워크
  - eXtreme Programming
  - Scrum

<aside>
➿ Agile, 근데 Waterfall을 곁들인 ⇒ TDD

</aside>

릴리스 주기

### ⏰ eXtreme Programming

- 시간에 대한 것
- 개발자가 시간 단위로 무엇을 할 것인가
  - 초단위 : Pair Programming
    - 개발자 간 능력의 차이를 줄여 준다.
  - 분단위 : Unit Test
    - Functionally Test : 기능 테스트 (의도한 대로 동작)
    - 실패 시나리오 통과 테스트 (의도한 대로 실패)
  - 일 단위로 Acceptance Test를 진행
  - 주 단위로 이 iteration을 반복
- Key Process
  - Key Role : PM, Technical Writer, Interaction Designer, Test, Programmer, User …
  - Planning : 2주 주기. 프로토타입을 통해 개발 방향 점검
  - TDD : Test Code → 기능 개발 → 테스트로 검증
  - Pair Programming : Drive & Navigator

### 📝 Scrum

- 태스트에 대한 것
- 상호, 점진적 개발방법론
- 개발할 기능, 수정 사항에 대해 우선 순위를 부여하고 이 순서대로 Task 진행
- 매일 15분의 회의 진행
  - 데일리 스크럼
    - PM이 진행상황을 체크해서 스크럼 모듈을 관리
- 1-4주의 Sprint(기획~리뷰)
  - 주기는 보통 2주
  - 하나의 스프린트에 대해 스프린트 백로그
  - 플래닝 포커, 스크럼 포커, 애자일 포커
    - 개발 목표를 위한 공수 산정, 상대적 규모 산정
    - 독립적으로 사고하고 제안하는 환경을 제공
    - 초심자에게는 쉽지 않다. 초심자는 그냥 달려가라
- Key Process
  - Key Role : Product Owner, Scrum Master(중간 다리 + documentation, Agile master..), Developer
  - Product Backlog : 제품 전체의 요구사항(Task)
  - Planning meeting
    - 스프린트 이전에 미팅을 통해 주기를 설정하고 할 일을 리스트업
  - Sprint Backlog : 해당 스프린트 요구사항(Task)
  - Daily Scrum
    - Retro Inspection
    - SWOT 분석
    - 3L 전략 : Liked Learned Lacked

<aside>
➿ Scrum with XP

</aside>

- Sprint 주기 : 2주
- 요구사항 분석 → 설계 → 구현(Scrum with XP)
  - Waterfall로 진행하되 구현은 애자일하게
  - Planning Meeting, Sprint Backlog, Daily Scrum, Test-Driven Development

### Before Implementation

- Requirement Analysis
  - Client
  - Functional
  - External interface
- Wireframe, Usecase, Storyboard
  - AdobeXD, Sketch, Framer …
  - Wireframe : 큰 그림 스케치
  - Usecase : 요구사항들에 대해 사용자가 어떤 일을 할 수 있는지 나열한 문서
    - UX 상에서 사용자의 travel time을 줄이기 위해
    - Actor 별로,
      - 일 간의 관계들 설정
      - Base Use Case
  - Design Prototype
- Data Flow, ERD
- API Design

### Tools

Communication : Slack

Repository : Github

Version management : git

Design : Figma

Diagram Tool : Drawio

Presentation : Marp

Documentation : .md in repository
