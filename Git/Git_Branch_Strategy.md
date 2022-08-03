# Git Branch Strategy

## Branch

- 분기점을 생성하여 독립적으로 코드를 변경할 수 있도록 도와주는 모델

`master`

```js
console.log("hello world");
```

`develop`

```js
console.log("I'm Jiseung");
```

## Branch 관련 Command

Show available **local branch**
`$ git branch`

Show available **remote branch**
`$ git branch -r`

Show available **All branch**
`$ git branch -a`

Create branch
`$ git branch stem`

Checkout branch
`$ git checkout stem`

Create & Checkout branch
`$ git checkout -b new-stem`

> 이제는 이렇게 쓰자
> `$ git switch -c new-stem`

`$ git commit -a -m 'edit readme.md'`

`$ git checkout master`

merge branch
`$ git merge stem`

delete branch
`$ git branch -D stem`

push with specified remote branch
`$ git push origin stem`

see the difference between two branches
`$ git diff master stem`

## Branching models

- git flow
  - (hotfix)- `master` -(release)- `develop` - feature
  - pros: 가장 많이 적용, 각 단계가 명확히 구분
  - cons: 복잡..
- github flow
  - `master` - feature
  - pros: 브랜치 모델 단순화, `master`의 모든 커밋은 deployable
  - cons: CI 의존성 높음. 누구 하나라도 실수했다간..(pull request로 방지)
- gitlab flow
  - `production` - `pre-production` - `master` - feature
  - pros: deploy, issue에 대한 대응이 가능하도록 보완
  - cons: git flow와 반대 (`master`develop, `production`master)
