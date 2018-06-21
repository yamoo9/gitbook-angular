# 라우트 설정

### 라우터 모듈 {#modules}

Angular에서 제공하는 라우터 모듈를 사용해 [싱글 페이지 애플리케이션\(SPA\)](https://ko.wikipedia.org/wiki/%EC%8B%B1%EA%B8%80_%ED%8E%98%EC%9D%B4%EC%A7%80_%EC%95%A0%ED%94%8C%EB%A6%AC%EC%BC%80%EC%9D%B4%EC%85%98)를 구현할 수 있습니다. 아래 링크를 통해 각 모듈에 대한 레퍼런스를 확인할 수 있습니다.

* [RouterModule](https://angular.io/api/router/RouterModule)
* [Router](https://angular.io/api/router/Router)
* [RouterOutlet](https://angular.io/api/router/RouterOutlet)
* [RouterLink](https://angular.io/api/router/RouterLink)
* [RouterLinkWithHref](https://angular.io/api/router/RouterLinkWithHref)
* [RouterLinkActive](https://angular.io/api/router/RouterLinkActive)

### 기본 href 설정 {#base-href}

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
라우터는 HTML5 pushState 전략을 기본으로 사용 하므로 기본 패스를 설정해야 합니다. 사용자가 URL을 임의로 복사하여 붙여넣는 경우\(deep-linking\)에 대응하기 위한 필수 조치입니다. 보다 자세한 내용은 [Routing & Navigation 페이지의 base href 설정 섹션](https://angular.io/guide/router#base-href)을 참고해서 읽어보세요.
{% endhint %}

### 라우트 설정 {#routes}

Angular 라우트 모듈 `RouterModule`, `Routes` 를 `@angular/router`에서 불러온 후, 라우트를 설정합니다. 라우트는 배열 내부에 `path`, `compoent` 속성을 가진 객체를 통해 각 패스\(Path\)에 따라 표시될 컴포넌트를 설정합니다.

{% code-tabs %}
{% code-tabs-item title="app.module.ts" %}
```typescript
// Routes, RouterModule 모듈 로드
import { RouterModule, Routes } from '@angular/router';

// 라우트 설정
const routes:Routes = [
  { path: '', component: AppComponent },
  { path: 'search', component: SearchComponent },
];
```
{% endcode-tabs-item %}
{% endcode-tabs %}

설정된 라우터가 애플리케이션의 루트에 제공되기 때문에 `forRoot()` 메서드를 통해 `routes`를 설정해야 합니다. `forRoot()` 메서드는 라우팅에 필요한 라우터 서비스 제공자\(Providers\)와 디렉티브를 공급하고, 현재 브라우저 URL을 토대로 초기 내비게이션을 수행합니다.

{% code-tabs %}
{% code-tabs-item title="app.module.ts" %}
```typescript
@NgModule({
  imports: [
    // 라우트 모듈 forRoot() 설정
    RouterModule.forRoot(routes, { useHash: true })
  ]
})
export class AppModule() {}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% hint style="info" %}
패스 로케이션 전략\(Path Location Strategies\)으로 URL에 해시\(\#\)를 사용하고자 한다면 useHash 값을 true로 설정합니다. \(기본 값: false\)

```typescript
https://service-domain.io/#
https://service-domain.io/#/search
```
{% endhint %}

### 라우터 아웃렛 디렉티브 {#router-outlet}

라우터 아웃렛\(배출구\) 디렉티브는 패스에 설정된 컴포넌트를 렌더링할 영역입니다. 라우터 설정된 패스에 따라 해당 컴포넌트가 표시됩니다.

{% code-tabs %}
{% code-tabs-item title="app.component.html" %}
```markup
<app-header></app-header>
<div class="routing-output-area">
  <router-outlet></router-outlet>
</div>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### 리디렉션 {#redirection}

패스를 구성하는 방법은 몇 가지가 있습니다. 예를 들어 경로를 변경하여 다음과 같은 [리디렉션](https://ko.wikipedia.org/wiki/%EB%A6%AC%EB%8B%A4%EC%9D%B4%EB%A0%89%EC%85%98)을 추가 할 수 있습니다. `redirectTo` 속성은 설정된 패스로 URL이 변경 되었을 때, 사용자에게 보여질 패스로 리디렉션 처리 합니다.

```typescript
const routes:Routes = [
  { path: 'home', component: HomeComponent },
  { path: 'search', component: SearchComponent },
  { path: 'find', redirectTo: 'search' },
  { path: '', redirectTo: 'home', pathMatch: 'full' },
];
```

{% hint style="info" %}
pathMatch 속성으로 'full'을 사용하면 패스가 완전히 일치할 때 리디렉션 됩니다. \(기본 값: prefix\)
{% endhint %}

### 와일드 카드 {#wildcard}

별도로 설정되지 않은 패스 에는 와일드 카드\(\*\*\)를 사용하여 특정 컴포넌트를 표시하도록 설정할 수 있습니다. 예를 들어 설정되지 않은 패스로 접속을 시도한 경우 404 오류 컴포넌트를 화면에 표시할 수 있습니다.

```typescript
const routes:Routes = [
  { path: 'home', component: HomeComponent, },
  { path: 'search', component: SearchComponent, },
  { path: 'find', redirectTo: 'search', },
  { path: '', redirectTo: 'home', pathMatch: 'full' },
  { path: '**', component: Error404Component, },
];
```

![404 &#xC624;&#xB958; &#xD398;&#xC774;&#xC9C0; &#xB514;&#xC790;&#xC778;](../.gitbook/assets/image%20%2820%29.png)

