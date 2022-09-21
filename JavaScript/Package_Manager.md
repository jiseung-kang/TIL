# JavaScript의 Package Manager

> JavaScript 패키지 매니저에는 크게 npm, yarn(yarn berry), pnpm이 있다.

## 패키지 매니저가 하는 일

- 메타데이터 처리 및 쓰기
- 모든 종속성을 일괄 설치 또는 업데이트
- 종속성 추가, 업데이트 및 제거
  - npm과 yarn은 node_modules 폴더에 종속성을 설치한다.
  - pnpm은 node_modules에 종속성을 보다 효율적으로 저장하는 새로운 개념들을 도입했다.
  - yarn berry는 더 나아가 node_modules를 완전히 PnP모드로 전환했다.
- 스크립트 실행
- 패키지 게시
- 보안 감사 수행

## History

### 패키지 이슈

- 서로 다른 의존관계 해결 알고리즘
- 보안에 영향을 미치는 호이스트 지원
- 성능에 영향을 미치는 다양한 lock 파일 형식
- 패키지를 디스크에 저장하는 각기 다른 방식
- 다중 패키지 프로젝트(워크스페이스) 지원
- 새로운 툴과 명령어에 대한 다양한 요구
- 다양한 수준의 구성과 유연성

## npm

> npm은 사실 Node Package Manager의 약자가 아니다..
> **npm is not an acronym**의 재귀적인 약자이다.
> pm이라는 이름의 bash 유틸리티는 다양한 플랫폼에 다양한 것을 설치하는 bash 함수 pkgmakeinst의 줄임말
> node pm 또는 new pm이라고 하는 것이 옳다.
> Node.js 런타임에 번들러되어 있다.

Github이 npm을 인수했다. 메이저 버전은 2021.10 v8이다.

2016.10 Facebook은 Google 등과 npm의 일관성, 시큐러티, 퍼포먼스 문제를 해결할 새로운 패키지 매니저 개발을 발표했고 이를 Yarn(Yet Another Resource Negotiator)이라고 정했다.

## Yarn

Yarn 아키텍처 설계는 npm에 기초하지만, 패키지 매니저의 환경에 큰 영향을 미쳤으며 다음을 추가했다.

- 기본 모노레포 지원
- 캐시를 인식한 설치
- 오프라인 캐싱
- 파일 잠금

Yarn v1은 2020년부터 유지 관리 모드로 들어가 Yarn Classic으로 이름이 바뀌었다.

후속으로 Yarn v2, Yarn Berry가 현재 활성 개발 분기다.

## pnpm

pnpm은 npm에 대한 drop-in 대체로, npm 프로젝트가 있으면 바로 pnpm을 사용할 수 있다.

pnpm이 npm, yarn에 대해 느낀 문제는 종속성의 중복 저장소였다.

Yarn Classic은 npm보다 빠르지만 동일한 종속성을 가지고 있다. npm, Yarn Classic은 모두 호이스팅을 지원한다.

pnpm은 호이스팅 대신 콘텐츠 주소 지정 가능 스토리지를 도입했다. 이 방법으로 node_modules 홈 폴더의 전역 저장소에 패키지를 저장하는 중첩 폴더가 생성된다. 종속성의 모든 버전은 이 폴더에 물리적으로 한번만 저장되어 단일 소스를 구성하고 디스크 공간을 절약한다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ae3619d5-4895-43f9-bc03-8342e2be6a44/Untitled.png)

## Yarn(v2, Berry), PnP

Yarn 2는 새로운 원칙의 새로운 패키지 관리자임을 명시하기 위해 Yarn Berry라고 명명했다.

주요 변경은 node_modules를 수정하는 전략으로 PnP 접근 방식을 사용한 것인데, 중첩된 폴더를 생성하는 대신 종속성 조회 테이블이 있는 단일 파일을 생성하고 모든 패키지는 폴더 내부에 zip파일로 관리한다.

다만 이 변경 사항으로 호환성에 대한 논란이 있었고, 후속 릴리스에서 node_modules 플러그인으로 호환성을 해결했다. 또한 JavaScript가 PnP 지원을 점점 더 많이 제공해 Yarn Berry가 더욱 활성화되었다.

pnpm은 2020년 말에 PnP 방식을 채택했다.

## 설치

npm는 Node.js와 함께 제공되므로 추가 단계가 필요하지 않다.

Yarn은 `npm i -g yarn`으로 설치한다.

Yarn Classic을 Yarn Berry로 마이그레이션하려면 Yarn Classic을 업데이트하거나 `yarn set version berry`를 사용한다. 가장 권장되는 방법은 Corepack을 활용하는 것이다. Corepack은 Node.js 최신 버전에 설치되어있으며, Corepack을 사용하면 대체 패키지 관리자를 별도로 설치하지 않아도 된다.

pnpm은 npm 패키지로 설치 `npm i -g pnpm`하거나 Corepack으로 설치`corepack prepare pnpm@6.24.2 —activate`할 수 있다.

## 프로젝트 구조

모든 패키지 관리자는 모든 중요한 메타 정보를 프로젝트 매니페스트 파일 `package.json`에 저장한다. 또한 루트 수준의 구성 파일을 사용해 개인 레지스트리, 종속성 해결 방법을 설정할 수 있다.

설치 단계에서 종속성은 파일 구조에 저장되고 잠금 파일이 생성된다.

- npm
  - npm install로 package-lock.json파일과 node_modules 폴더 생성
  - 선택적 .npmrc 구성 파일을 루트 수준에 배치할 수 있다.
- Yarn Classic
  - yarn 으로 yarn.lock과 node_modules가 생성된다.
  - 선택적 .yarnrc
  - .npmrc도 존재한다.
  - 선택적으로 캐시폴더 .yarn/cache/와 버전 저장 .yarn/releases/를 사용할 수 있다.
- Yarn Berry + node_modules
  - .npmrc, .yarnrc를 사용하지 않는다.
  - .yarnrc.yml 구성 파일을 설정해 nodeLinker 구성을 제공해야 한다.
  - yarn을 실행하면 모든 종속성이 설치되고 Yarn Classic에 호환되지 않는 파일이 생성된다.
- Yarn Berry + PnP
  - 엄격한 PnP 모드가 기본이며, 느슨한 PnP도 지원한다.
- pnpm
  - pnpm 프로젝트는 npm, Yarn Classic의 초기 상태와 비슷하게 package.json이 필요하다.
  - pnpm i로 종속성을 설치하면 node_modules가 생성되는데 폴더 구조가 완전히 다르다.
  - 자체 잠금 파일인 pnp-lock.yml와 선택적 .npmrc을 사용해 추가 구성을 제공할 수 있다.

## 파일 및 종속성 저장소 lock

모든 패키지 관리자는 잠금 파일을 생성한다.

잠금 파일은 프로젝트에 대해 설치된 각 종속성 버전을 정확히 저장해 보다 예측 가능한 설치가 가능하다.

버전을 잠그지 않으면 실제로 설치된 버전이 다를 수 있다.

npm, Yarn Classic, pnpm은 종속성이 폴더 구조에 설치된다.

PnP 모드의 Yarn Berry는 종속성을 .yarn/cache/, .pnp.cjs 파일의 조합으로 zip 파일에 저장한다.

## 구성 파일

패키지 관리자 구성은 package.sjon 전용 구성 파일에 있는데, 구성 옵션의 예는 다음과 같다.

- 사용할 정확한 버전
- 특정 종속성 해결 전략
- 비공개 레지스트리에 대한 엑세스 구성
- monorepo 내 작업 영역을 찾을 위치

npm : .npmrc. package.json에서 workspaces를 구성해 위치를 알린다. 이는 공개 레지스트리와 함께 작동하며 개인 레지스트리를 구성하려면 .npmrc에서 수행해야 한다.

Yarn Classic : package.json에서 작업 영역을 설정할 수 있고 이는 개인 패키지(private: true)여야 한다. 선택적 구성은 .yarnrc 파일에 있으며 공유하기 위해 특정 바이너리 버전을 적용하는 yarn-path를 설정하는 것이 일반적이다.

Yarn Berry : package.json을 사용하고 .yarnrc.yml에서 구성 옵션을 사용할 수 있다. 메타데이터 필드의 이름이 yarnPath로 변경되었다. 비호환성으로 PnP 엄격 모드에서 종속성에 문제가 있을 수 있다.

pnpm : npm과 동일한 구성 메커니즘을 사용하므로 .npmrc 파일을 사용할 수 있다. 개인 레지스트리 구성도 npm과 동일하다. workspace로 다중 패키지 프로젝트를 지원할 수 있고 pnpm-workspace.yaml으로 패키지 위치를 지정해 모노레포지토리를 초기화할 수 있다.

## 모노 레포

모노레포, 모노 레포지토리란 작업 공간 또는 패키지라고 하는 여러 프로젝트를 보관하는 레포지토리다. 여러 레포지토리를 사용하는 대신 모든 것을 한 곳에 보관하는 프로젝트 조직 전략으로, 주요 패키지 관리자가 작업 공간 기능을 제공한다.

- npm
  - v7부터 npm 작업 공간 기능을 출시했다.
  - 루트 패키지 내에서 다중 패키지 프로젝트를 관리하는 데 도움되는 여러 cli 명령이 포함되어 있다.
  - v8은 고급 필터링이나 여러 작업 영역 관련 명령을 병렬로 실행하는 것을 지원하지 않는다.
- Yarn Classic
  - workspace 측면에서 최고 수준의 monorepo 지원을 발표했다. (2017)
  - Yarn의 추가 기능은 다른 패키지 관리자에도 이러한 기능을 구현할 수 있는 길을 열었다.
- Yarn Berry
  - Yarn Classic 개념 기반. workspace를 특징으로 한다.
  - yarn add -interactive : 패키지를 설치할 때 다른 작업 공간의 버전을 재사용할수 있다.
  - yarn up : 모든 작업 공간에서 패키지 업데이트
  - yarn workspaces focus : 단일 작업 공간에만 종속성 설치
  - yarn workspaces foreach : 모든 작업 공간에서 명령 실행
  - 파일 필드에서 사용할 수 있는 프로토콜을 많이 사용한다.
  - 종속성이 모노레포의 패키지 중 하나여야 한다고 명시
  - 그렇지 않으면 버전이 일치하지 않을 때 원격 레지스트리에서 버전을 가져오게 할 수 있다.
- pnpm
  - 프로토콜을 통해 Yarn Berry와 유사하게 monorepo 프로젝트를 용이하게 한다.
  - pnpm 명령은 monorepo 컨텍스트에서 특히 유용한 —recursive, filter 등의 옵션을 허용한다.

## 보안

npm은 모든 패지지에 너무 관대해 보안 취약점이 있다. 최신 npm 버전에서는 SHA-512 암호화 알고리즘을 사용해 패키지 무결성을 확인한다.

Yarn Classic, Yarn Berry는 저장된 체크섬으로부터 각 패키지의 무결성을 확인했다.

yarn.lock은 설치 중 선언되지 않은 악성 패키지를 검색하지 못하게 방지한다.

PnP 모드의 Yarn Berry는 기존 접근 방식의 보안 문제를 겪지 않는다.

pnpm은 코드가 실행되기 전에 모든 패키지의 무결성을 확인하기 위해 체크섬을 사용한다. npm과 Yarn Classic은 호이스팅으로 인한 보안 문제가 있는데, pnpm은 모델이 호이스팅을 사용하지 않고 대신 중첩 폴더를 생성함으로써 종속성이 명시적인 경우에만 다른 종속성에 액세스할 수 있도록 한다.

## 결론

pnpm는 cli가 비슷해 npm처럼 보이지만 종속성을 관리하는 많은 것이 다르며, 더 나은 성능과 디스크 공간 효율성으로 이어진다.

Yarn Classic은 인기있지만 레거시 소프트웨어로 가까운 시일 내에 지원이 중단될 수 있다.

Yarn Berry PnP는 잠재력을 완전히 실현하지 못했지만 관심을 가지기에 충분하다.

### 참고 자료

[JavaScript package managers compared - npm, Yarn, or pnpm?](https://doppelmutzi.github.io/packageManagers/)
