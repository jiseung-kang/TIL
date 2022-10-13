# 컴포넌트 결합

컴포넌트 구조와 관련된 아키텍처를 침범하는 힘은 기술적이며 정치적이고 가변적이다.

### ADP: 의존성 비순환 원칙

> 컴포넌트 의존성 그래프에 순환이 있으면 안된다.

1. Weekly Build (주 단위 빌드)

- 4일 개발, 1일 통합
  - 개발 < 통합 : 효율성 저하
  - 빌드 주기를 낮추면? 통합과 테스트, 빠른 피드백이 어렵다.

1. ADP(의존성 비순환 원칙) : 순환 의존성 제거하기

- 개발 환경을 릴리스 가능한 컴포넌트 단위로 분리
  - 컴포넌트 : 개별 개발자, 단일 개발팀이 책임질 수 있는 작업 단위
  - 통합은 작고 점진적으로 이뤄진다.
  - 이를 위해 의존성 구조에 순환이 있으면 안된다.
  - 컴포넌트 간의 의존성 구조 : 비순환 방향 그래프
- 전체 릴리스 절차를 상향식으로 진행한다.
- 순환이 컴포넌트 의존성 그래프에 미치는 영향
  - 순환 의존성 : 호환성 ⇒ 릴리스의 어려움.
  - 동일한 릴리스를 사용해야하므로 서로에게 얽매이게 된다.
  - 이 경우 컴포넌트를 분리하기 어렵고, 모듈 개수에 따라 빌드 관련 이슈가 증가한다.
- 순환 끊기 : 순환을 끊고 의존성을 다시 DAP로 원상복구
  1. DIP(의존성 역전 원칙)으로 순환을 끊기
  2. 모두 의존하는 새로운 컴포넌트를 만들어 이동시키기
- 흐트러짐(Jitters)
  - 요구사항이 변경되면 컴포넌트 구조도 변경될 수 있다.
  - 의존성 구조에 순환이 발생하는지 관찰하고, 끊어내야 한다.

### 하향식(top-down) 설계

> 결국 컴포넌트 구조는 하향식으로 설계될 수 없다.

컴포넌트 의존성 다이어그램은 애플리케이션의 빌드 가능성과 유지보수성을 보여주는 지도와 같다.

의존성 구조와 관련된 최우선 관심사는 변동성을 격리하는 일

컴포넌트 의존성 그래프는 자주 변경되는 컴포넌트로부터 안정적이며 가치가 높은 컴포넌트를 보호하려는 아키텍트가 만들고 가다듬게 된다.

애플리케이션이 성장함에 따라 CRP가 영향을 미치고, 순환이 발생하면 ADP가 적용된다.

이 과정에서 흐트러지고, 성장한다.

### SDP: 안정된 의존성 원칙

> 안정성의 방향으로 더 의존하라

설계는 정적일 수 없으며 변경은 불가피하다.

CRP를 준수하면서 컴포넌트가 다른 유형의 변경에는 영향받지 않으면서 특정 유형의 변경에만 민감하게 만들 수 있다.

- 안정성
  - 쉽게 움직이지 않는
  - 안정성의 지표
    - Fan-in : 안으로 들어오는 의존성. 컴포넌트 내부의 클래스에 의존하는 컴포넌트 외부의 클래스 개수
    - Fan-out : 밖으로 나가는 의존성. 컴포넌트 외부의 클래스에 의존하는 컴포넌트 내부의 클래스 개수
    - I = Fan-out / (Fan-in + Fan-out) (0이면 최고로 안정된 컴포넌트, 1이면 최고로 불안정한 컴포넌트)
    - I가 1이면 어떤 컴포넌트도 해당 컴포넌트에 의존하지 않지만, 해당 컴포넌트는 다른 컴포넌트에 의존한다. 이 컴포넌트는 책임성이 없으며 의존적이다. 이 컴포넌트를 맘껏 변경할 수 있지만, 그 대상을 언젠가 변경해야할 이유가 생긴다.
    - I가 0이면 해당 컴포넌트에 의존하는 다른 컴포넌트가 있지만, 이 컴포넌트 자체는 다른 컴포넌트에 의존하지 않는다. 이 컴포넌트는 다른 컴포넌트를 책임지며, 독립적이다. 변경이 어렵지만 변경을 강제하는 의존성이 없다.
  - SDP에서 컴포넌트의 I 지표는 그가 의존하는 다른 컴포넌트의 I보다 커야한다.
  - 즉 의존성 방향으로 갈 수록 I 지표가 감소해야 한다.
- 모든 컴포넌트가 안정적이어야 하는 것은 아니다.
  - 불안정한 컴포넌트도 있고 안정된 컴포넌트도 있다.
  - 불안정한 컴포넌트를 관례적으로 위쪽에 두고, 위로 향하는 화살표가 없도록 다이어그램을 그려보자
  - DIP를 도입하면 의존하는 두 컴포넌트를 다른 인터페이스에 의존하도록 강제해 의존성이 I가 감소하는 방향으로 흐르게 할 수 있다.
  - 추상 컴포넌트
    - 자바, C# 등의 정적 타입 언어에서 필요한 전략. 안정적이며, 덜 안정적인 컴포넌트가 의존할 수 있는 이상적인 대상
    - 동적 타입 언어에서는 이러한 의존성이 전혀 없다. 인터페이스를 선언하고 상속받는 일이 필요없다.

### SAP: 안정된 추상화 원칙

> 컴포넌트는 안정된 정도만큼만 추상화되어야 한다.

- 고수준 정책을 어디에 위치시켜야 하는가?
  - 자주 변경하면 안되는 소프트웨어. 변동성이 없기를 기대
  - 고수준 정책을 캠슐화하는 소프트웨어는 반드시 I=0에 위치
  - 대신 이를 포함하는 소스 코드는 수정이 어려워진다.
  - 컴포넌트가 안정되면서도 변경에 유연하게? OCP 추상 클래스
- SAP(안정된 추상화 원칙) : 안정성과 추상화 정도의 관계
  - 안정된 컴포넌트는 추상 컴포넌트
  - 안정성이 컴포넌트를 확장하는 일을 방해하면 안된다.
  - 불안정한 컴포넌트는 반드시 구체 컴포넌트여야 쉽게 변경이 가능하다.
  - 안정적인 컴포넌트 : 인터페이스와 추상 클래스로 구성되어 쉽게 확장이 가능
  - DIP = SAP + SDP
    - SDP : 의존성이 반드시 안정성의 방향으로 향해야 한다.
    - SAP : 안정성이 결국 추상화
    - ⇒ 의존성은 추상화의 방향으로 향한다.
    - 하지만 DIP는 클래스의 원칙. 클래스는 추상적이거나 아니거나
    - 컴포넌트는 어떤 부분은 추상적이면서 다른 부분은 안정적일 수 있다.
- 추상화 정도 측정하기
  - 컴포넌트의 클래스 총 수 대비 인터페이스와 추상 클래스의 개수
  - 주계열 : 파생 클래스는 추상적이면서 의존성을 가질 수 있다.
    - Zone of Exclusion = Zone of Uselessness + Zone of Pain
    - 고통의 구역 : 매우 안정적이면서 구체적. 확장할 수 없고 변경할 수 없다. 스키마, 유틸리티 라이브러리
    - 쓸모없는 구역 : 최고로 추상적이면서 의존하지 않는다. 여기는 폐기물
    - 벗어나기 : 너무 추상적이지도, 불안정하지도 않다.
  - 주계열과의 거리 : 얼마나 떨어져있는가?
    - 0이면 가장 가깝고
    - 1이면 가장 멀다.
    - 자신에게 의존하는 컴포넌트가 거의 없는데 너무 추상적이거나 자신에게 의존하는 컴포넌트가 많은데 너무 구체적이거나

### 결론

좋은 의존성과 좋지 않은 의존성이 있다.