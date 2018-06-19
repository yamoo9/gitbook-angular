# 클라이언트 사이드 라우팅

## 라우터 모듈

Angular 라우터\(Routers\)를 사용해 [싱글 페이지 애플리케이션\(SPA\)](https://ko.wikipedia.org/wiki/%EC%8B%B1%EA%B8%80_%ED%8E%98%EC%9D%B4%EC%A7%80_%EC%95%A0%ED%94%8C%EB%A6%AC%EC%BC%80%EC%9D%B4%EC%85%98)를 구현할 수 있습니다.

* [RouterModule](https://angular.io/api/router/RouterModule)
* [Router](https://angular.io/api/router/Router)
* [RouterOutlet](https://angular.io/api/router/RouterOutlet)
* [RouterLink](https://angular.io/api/router/RouterLink)
* [RouterLinkWithHref](https://angular.io/api/router/RouterLinkWithHref)
* [RouterLinkActive](https://angular.io/api/router/RouterLinkActive)

### 기본 href 설정

대부분의 라우팅 애플리케이션은 `<base>`요소를 추가하여 라우터에 탐색 URL을 작성하는 방법을 알려줘야 합니다.

{% code-tabs %}
{% code-tabs-item title="index.html" %}
```markup
</head>

  <base href="/">
</head>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% hint style="info" %}
기본 href 설정은 필수입니다. 보다 자세한 내용은 [Routing & Navigation 페이지의 base href 설정 섹션](https://angular.io/guide/router#base-href)을 참조하세요.
{% endhint %}

### 라우트 설정



{% code-tabs %}
{% code-tabs-item title="app.module.ts" %}
```typescript
// Routes, RouterModule 모듈 로드
import { RouterModule, Routes } from '@angular/router';

// 라우트 설정
const routes:Routes = [
  { path: '', component: AppComponent },
  { path: 'search', component: SearchComponent }
];

@NgModule({
  imports: [
    // 라우트 모듈 forRoot() 설정
    RouterModule.forRoot(routes)
  ]
})
export class AppModule() {}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% hint style="info" %}
설정된 Router가 앱의 루트에 제공되기 때문에 forRoot\(\) 메서드를 호출합니다. forRoot\(\) 메서드는   
라우팅에 필요한 Router Service providers와 Directive를 제공하고 현재 브라우저 URL을 기반으로   
초기 Navigation을 수행합니다.
{% endhint %}

