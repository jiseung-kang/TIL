# 경계 해부학

시스템 아키텍처는 일련의 소프트웨어 컴포넌트와 그 컴포넌트를 분리하는 경계에 의해 정의

## 경계 횡단하기

런타임에 경계를 횡단 = 그저 데이터를 전달하는 것

적절한 위치에서 횡단하도록 하는 것 ? 소스 코드 의존성 관리

경계는 방화벽을 구축하고 관리하는 수단

## 두려운 단일체

물리적으로 엄격하게 구분되지 않는 형태, 소스 수준 분리 모드

단일체는 경계가 드러나지 않는데, 그 안에서 독립성을 유지하는 건 가치있는 일

- 동적 다형성에 의존해 내부 의존성을 관리 (객체 지향)
- 저수준 클라이언트에서 고수준 서비스로 향하는 함수 호출
- 고수준 클라이언트가 저수준 서비스를 호출해야 한다면 동적 다형성을 사용해 의존성 역전
- 규칙적인 방식의 구조 분리는 도움이 된다.

## 배포형 컴포넌트

동적 링크 라이브러리는 경계가 물리적으로 드러난다.

컴파일 없이 사용할 수 있지만, 컴포넌트는 바이너리와 같이 배포 가능한 형태로 전달

배포 수준 결합 분리 모드

런타임 로딩이 오래걸릴 수 있지만 결계를 가로지르는 통신 빈번

## 스레드

단일체, 배포형 컴포넌트 모두 스레드 활용이 가능하다.

스레드는 실행 계획과 순서를 체계화하는 방법

모든 스레드가 단 하나의 컴포넌트에 포함 될 수도, 많은 컴포넌트에 걸쳐 분산될 수도

## 로컬 프로세스

강한 물리적 형태를 띠는 아키텍처 경계

명령행이나 유사한 시스템 호출을 통해 생성

대부분 소켓, 메일박스, 메시지 큐 등의 통신 기능으로 통신한다.

정적 링크 단일체거나, 동적 링크 여러 컴포넌트거나

## 서비스

물리적 형태를 띠는 가장 강력한 경계

프로세스

명령행, 시스템 호출로 구동된다.

자신의 물리적 위치에 구애받지 않는다.

통신이 함수 호출에 비해 느리며, 통신 지연 문제는 고수준에서 처리할 수 있어야 한다.

저수준 서비스는 반드시 고수준 서비스에 플러그인 되어야 한다.

## 결론

단일체를 제외한 대다수 시스템은 한가지 이상의 경계 전략을 사용한다.

서비스는 상호작용하는 일련의 로컬 프로세스 퍼사드에 불과할 때가 많다.

개별 서비스, 로컬 프로세스는 거의 언제나 소스 코드 컴포턴트로 구성된 단일체이거나 동적으로 링크된 배포형 컴포넌트의 집합

통신이 빈번한 로컬 경계와 지연을 중요하게 고려해야 하는 경계가 혼합되어 있다.
