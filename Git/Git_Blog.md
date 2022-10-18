# Hexo로 나만의 Git Blog 만들기

## Github Pages

github 저장소를 활용해 정적인 사이트 호스팅이 가능하다.

name of repo : `username`.github.io

---

### 시작하기

`$ git clone <https://github.com/username/username.github.io.git`>

`$ git add .$ git commit -m "first page"$ git push origin master`

### sample index page

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <title>My first gh page</title>
  </head>
  <body>
    <h1>Home</h1>
    <p>Hello, there!</p>
  </body>
</html>
```

---

### Static Site Generator

- [Jekyll](https://jekyllrb.com/): Ruby 기반 정적인 블로그 생성기
  - 설치와 사용이 쉽다.
  - 사용자가 많다.
- [Hugo](https://gohugo.io/): Golang 기반 정적인 블로그 생성기
  - 빠른 속도로 사이트를 생성할 수 있다.
  - 사용자 증가 중
- [Hexo](https://hexo.io/): Node.js 기반 정적인 블로그 생성기
  - Node.js를 안다면 커스터마이징이 쉽다.
  - 빠른 속도로 사용자 증가 중

**Recommand** : `Hexo` > `Jekyll` > `Hugo`

---

## Hexo 시작하기

### Requirements

1. git
2. node.js([https://nodejs.org/en/](https://nodejs.org/en/))

`$ npm install -g hexo-cli`

---

## Init hexo project

```
$ hexo init <folder>
$ cd <folder>
$ npm install

```

## clean && generate static files

`$ hexo clean && hexo generate`

## Run hexo server

`$ hexo server`

---

## deploy

`$ npm install hexo-deployer-git --save`

```
deploy:
  type: git
  repo: <repository url>  branch: [branch] #published
  message:

```

---

## .gitignore and .gitattributes

### .gitignore: 특정파일 추적을 하고 싶지 않을 경우

```
*.java
*.py[cod]
```

### .gitattributes: 파일단위, 디렉토리 별 다른 설정을 부여하고 싶을 경우

```
# Avoid conflicts in pbxproj files
*.pbxproj binary merge=union

# Always diff strings files as text
*.strings text diff
```

- reference: [https://thoughtbot.com/blog/xcode-and-git-bridging-the-gap](https://thoughtbot.com/blog/xcode-and-git-bridging-the-gap)
