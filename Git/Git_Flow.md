# Git flow

## Git flow 시작하기

```bash
brew install git-flow-avh
```

시작할 git 저장소에서
`git flow init`으로 git flow 사용을 시작한다.
브랜치 명명규칙을 정할 때는 기본 값을 사용하기를 권장한다.

## Features

> 새 기능 개발하기

### 시작하기

```bash
git flow feature start MYFEATURE
```

`develop`에 기반한 새 기능 브랜치를 생성하고 그 브랜치로 전환한다.

### 끝내기

```bash
git flow feature finish MYFEATURE
```

- 새 기능 브랜치를 `develop`에 merge한다.
- 기능 브랜치를 삭제한다.
- `develop`브랜치로 전환한다.

### Publish

```bash
git flow feature publish MYFEATURE
```

기능을 원격 서버에 게시한다.

### Pull

```bash
git flow feature pull origin MYFEATURE
```

게시한 기능 가져오기

## Release

### 시작하기

```bash
git flow release start RELEASE [BASE]
```

`develop` 브랜치로부터 `release` 브랜치를 생성

### Publish & Track

```bash
git flow release publish RELEASE
```

```bash
git flow release track RELEASE
```

### 끝내기

```bash
git flow release finish RELEASE

git push --tages
```

- `release` 브랜치를 `master`브랜치에 merge
- 릴리스 이름으로 태그
- 릴리스를 `develop` 브랜치로 재병합
- `release` 브랜치 삭제

## Hotfixes

```bash
git flow hotfix start VERSION [BASENAME]
```

```bash
git flow hotfix finish VERSION
```
