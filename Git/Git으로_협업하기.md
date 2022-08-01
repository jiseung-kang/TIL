## Conventional Commits

ref: [https://www.conventionalcommits.org/ko/v1.0.0/](https://www.conventionalcommits.org/ko/v1.0.0/)

1.  commit의 제목은 commit을 설명하는 하나의 구나 절로 완성
2.  importanceofcapitalize => Importance of Capitalize
3.  **prefix** 꼭 달기
    -   **feat**: 기능 개발 관련
    -   **fix**: 오류 개선 혹은 버그 패치
    -   **docs**: 문서화 작업
    -   **test**: test 관련
    -   **conf**: 환경설정 관련
    -   **build**: 빌드 관련
    -   **ci**: Continuous Integration 관련

## Conventional Commits - example

> Commit Convention은 팀마다 다를 수 있으니 **관련 문서를 참조**할 것.

```
feat: Add server.py
fix: Fix Typo server.py
docs: Add README.md, LICENSE
conf: Create .env, .gitignore, dockerfile
BREAKING CHANGE: Drop Support /api/v1
refactor: Refactor user classes
```

## commit 할 때 기억해야 할 것

-   commit은 **동작 가능한 최소단위**로 자주 할 것
-   해당 작업단위에 수행된 모든 파일 변화가 해당 commit에 포함되어야 함
-   모두가 **이해할 수 있는 log**를 작성할 것
-   Open Source Contribution시 영어가 강제되지만, 그렇지 않을 경우 **팀 내 사용 언어**를 따라 쓸 것
-   **제목은 축약**하여 쓰되(50자 이내), **내용은 문장형**으로 작성하여 추가설명 할 것
-   제목과 내용은 한 줄 띄워 분리할 것
-   내용은 이 commit의 구성과 의도를 충실히 작성할 것

## Appendix

### .gitignore

[gitignore.io](https://www.toptal.com/developers/gitignore)

### LICENSE

-   MIT License
    -   MIT에서 만든 라이센스로, 모든 행동에 제약이 없으며, 저작권자는 소프트웨어와 관련한 책임에서 자유롭습니다.
-   Apache License 2.0
    -   Apache 재단이 만든 라이센스로, 특허권 관련 내용이 포함되어 있습니다.
-   GNU General Public License v3.0
    -   가장 많이 알려져있으며, 의무사항(해당 라이센스가 적용된 소스코드 사용시 GPL을 따라야 함)이 존재합니다.
