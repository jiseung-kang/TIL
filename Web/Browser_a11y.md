# 브라우저 웹 접근성 지원하기
## 지원하지 않는 브라우저

```html
<noscript>이 사이트를 이용하려면? 사용 중인 웹 브라우저에서 JavaScript를 활성화 해야 합니다.</noscript>
  
<!--[if IE]>
<div>
  안된다는 안내
</div>
<![endif]-->
```

- noscript
    - 모든 브라우저가 JavaScript를 지원하는 것은 아니다. 이러한 경우 안내(alternative text)가 필요하다.
- `<!--[if IE]>` … `<![endif]—>`
    - 해당 구문은 IE9 이하 버전 사용자에게 표시된다.
    - IE10 이상부터는 다른 방식의 안내가 필요하다.
    
    ```jsx
    // displayUpgradeInfo.js
    
    function renderUpgradeBrowserInfo() {
      const upgradeMarkup = '<div>안된다는 안내</div>';
      document.body.insertAdjacentHTML('afterbegin', upgradeMarkup);
    }
    
    document.documentMode && document.documentMode < 12 && renderUpgradeBrowserInfo();
    ```
    

## IE 지원 구문

```html
<meta http-equiv="X-UA-Compatible" content="IE=edge" />
```

## CSS

### 잊을만하면 웹 표준

`font: 1rem/1.5;`

line-height 1.5 이상이 웹 표준

### :root

<aside>
💡 문서 트리의 루트 요소를 선택한다.
HTML의 경우 루트 요소는 <html>

</aside>

CSS는 html 문서에만 적용되는 것이 아니라는 점을 알아두자