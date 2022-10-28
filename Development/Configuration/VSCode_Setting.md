# Setting.json에 대하여

```json
{
  // 파일 확장자와 언어를 연결
  "files.associations": {
    "*.js": "javascriptreact",
    // 이것 때문에 간혹 빨간 줄 뜨는 파일들이 있더라 (ex. npmrc)
    "*rc": "json"
  },
  // 파일 및 폴더를 제외. 이걸 기준으로 파일 및 폴더를 숨긴다.
  "files.exclude": {
    "**/.git": true,
    "**/.svn": true,
    "**/.hg": true,
    "**/CVS": true,
    "**/.DS_Store": true,
    "**/Thumbs.db": true,
    "**/node_modules": true,
    "**/*.js.map": {
      "when": "$(basename)"
    }
  },
  // 검색할 때 제외 항목
  "search.exclude": {
    "**/coverage": true,
    "**/node_modules": true
  },
  // 이건 커스텀으로 self closing 태그들을 명시해준 것
  "auto-close-tag.excludedTags": [
    "area",
    "base",
    "br",
    "col",
    "command",
    "embed",
    "hr",
    "img",
    "input",
    "keygen",
    "link",
    "meta",
    "param",
    "source",
    "track",
    "wbr"
  ],
  // emmet 스니펫에 사용될 변수
  "emmet.variables": {
    "charset": "UTF-8",
    "lang": "ko-KR"
  },
  // 언어와 emmet 사이 매핑을 지원해준다.
  "emmet.includeLanguages": {
    "markdown": "html",
    "mdx": "javascriptreact",
    "javascript": "javascriptreact",
    "typescript": "typescriptreact"
  },
  // tab으로 emmet 지원
  "emmet.triggerExpansionOnTab": true,
  // emmet 제안을 스니펫 제안처럼 지원해준다.
  "emmet.showSuggestionsAsSnippets": true,
  // emmet으로 사용 가능한 약어 표시
  "emmet.showExpandedAbbreviation": "always",
  // 고유한 프로필을 정의해준다.
  "emmet.syntaxProfiles": {
    "html": "xhtml",
    "inline_break": 3,
    "tag_case": "lower",
    "attr_case": "lower",
    "attr_quotes": "double",
    "self_closing_tag": "xhtml"
  },

  // 아래는 특정 언어에 대해 설정을 override하는 구문이다.
  "[html]": {
    "editor.defaultFormatter": "vscode.html-language-features",
    "editor.formatOnSave": false
  },
  "[css]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode",
    "editor.formatOnSave": false
  },
  "[javascript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[javascriptreact]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[json]": {
    "editor.defaultFormatter": "vscode.json-language-features"
  },
  "[jsonc]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[scss]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode",
    "editor.formatOnSave": true,
    "editor.quickSuggestions": {
      "comments": "on",
      "other": "on",
      "strings": "on"
    }
  },
  "[yaml]": {
    "editor.autoIndent": "advanced",
    "editor.insertSpaces": true,
    "editor.tabSize": 2
  },

  "html.autoClosingTags": true,
  // 힌트 표시
  // onUnlessPressed: Ctrl+Alt를 누르면 숨겨준다.
  // offUnlessPressed: Ctrl+Alt를 누르면 보여준다.
  "editor.inlayHints.enabled": "offUnlessPressed",

  "javascript.autoClosingTags": true,
  "javascript.suggest.autoImports": true,
  // 함수 시그니쳐를 채워준다.
  "javascript.suggest.completeFunctionCalls": true,

  // 힌트별 사용 가능 여부
  "javascript.inlayHints.variableTypes.enabled": true,
  "javascript.inlayHints.parameterNames.enabled": "all",
  "javascript.inlayHints.functionLikeReturnTypes.enabled": true,
  "javascript.inlayHints.propertyDeclarationTypes.enabled": true,
  "javascript.inlayHints.parameterNames.suppressWhenArgumentMatchesName": false,

  "javascript.format.enable": false,
  "javascript.validate.enable": false,

  "typescript.autoClosingTags": true,
  "typescript.suggest.autoImports": true,
  "typescript.suggest.completeFunctionCalls": true,
  "typescript.inlayHints.parameterNames.enabled": "all",
  "typescript.inlayHints.functionLikeReturnTypes.enabled": true,
  "typescript.format.enable": false,
  "typescript.validate.enable": false,

  "path-intellisense.extensionOnImport": true,
  "path-intellisense.mappings": {
    "@": "${workspaceRoot}/src"
  }
}
```
