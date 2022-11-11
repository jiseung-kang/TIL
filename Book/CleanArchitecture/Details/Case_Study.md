# 사례 연구 : 비디오 판매

## 제품

시스템의 초기 아키텍처를 결정하는 첫 단계는 액터와 유스케이스를 식별하는 일

## 유스케이스 분석

- 액터를 분리한다.
  - 단일 책임의 원칙
  - 시스템을 분할해 특정 액터를 위한 변경이 나머지 액터에게 영향을 미치지 않도록 한다.
- 추상 유스케이스
  - 범용적인 정책
  - 다른 유스케이스에서 이를 더 구체화
  - 유사성을 식별해 분석 초기에 통합 방법을 찾을 수 있다.

## 컴포넌트 아키텍처

- 뷰, 프레젠터, 인터랙터, 컨트롤러로 분리된 전형적인 분할 방법
- 컴파일과 빌드 환경 분리
  - 각 컴포넌트를 독립적으로 전달할 수 있게 빌드하는 것
- 뷰, 프레젠터, 인터랙터, 컨트롤러, 유틸리티 각각을 하나의 파일로
  - 독립적 배포
- 선택지를 열어주어 시스템의 변경 양상에 맞춰 시스템 배포 방식 조정

## 의존성 관리

- 입력이 컨트롤러에서 발생하면 인터랙터에 의해 처리되어 결과를 만든다.
- 프레젠터가 결과의 포맷을 변경하고 뷰가 화면에 표시
- 아키텍처가 의존성 규칙을 준수하면
  - 모든 의존성은 경계선을 한 방향으로만 가로지르는데
  - 항상 더 높은 수준의 정책을 포함하는 컴포넌트를 향한다.
- 개방 폐쇄 원칙
  - 사용관계는 제어흐름과 같은 방향
  - 상속 관계는 제어흐름과 반대 방향

## 결론

- 서로 다르게 변경되는 컴포넌트를 분리하기
  - 서로 다른 이유 : 단일 책임에 기반한 액터의 분리
  - 서로 다른 속도 : 의존성 규칙

⇒ 상황에 맞게 컴포넌트들을 배포 가능한 단위로 묶을 수 있고, 변환 상황에 맞춰 묶는 단위를 바꾸기도 쉬워진다.