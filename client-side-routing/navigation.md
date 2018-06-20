# 내비게이션

### href 내비게이션

href 속성에 URL 값을 할당해 애플리케이션 페이지로 내비게이션 할 수 있습니다. 각 링크를 클릭해 보면 클라이언트 사이드 렌더링에 따라 브라우저는 새로고침 되지 않고 빠르게 페이지와 URL을 변경합니다.

{% code-tabs %}
{% code-tabs-item title="app.component.html" %}
```markup
<nav>
  <ul class="nav justify-content-center">
    <li class="nav-item">
      <a class="nav-link active" href="/#/home">홈</a> 
    </li>
    <li class="nav-item">
      <a class="nav-link" href="/#/search">검색</a>
    </li>
  </ul>
</nav>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% hint style="warning" %}
useHash 옵션 설정 값이 true 일 경우, 클라이언트 사이드 렌더링이 적용됩니다. 만약 값이 false 일 경우는 각 링크 클릭 시, 매번 새로고침 됩니다. 즉, 서버 사이드 렌더링 처럼 처리됩니다.

```typescript
RouterModule.forRoot(routes, {useHash: false})

// useHash 기본 값은 false 이므로 위와 동일하게 처리 됩니다.
RouterModule.forRoot(routes)
```
{% endhint %}

### routerLink 디렉티브

routerLink 디렉티브를 사용해 패스 이름을 설정하여 내비게이션 하면 클라이언트 사이드 렌더링이 처리됩니다. 디렉티브는 일반적인 문자 값을 연결하는 방법과 속성 바인딩 방식을 사용합니다. 속성 바인딩 방식을 사용할 경우는 값으로 배열을 사용해야 합니다.

{% code-tabs %}
{% code-tabs-item title="app.component.html" %}
```markup
<nav>
  <ul class="nav justify-content-center">
    <li class="nav-item">
      <a class="nav-link" routerLink="home">홈</a> 
    </li>
    <li class="nav-item">
      <a class="nav-link" [routerLink]="['search']">검색</a>
    </li>
  </ul>
</nav>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### routerLinkActive 디렉티브

내비게이션 컴포넌트는 사용자에게 현재 활성화\(active\)된 항목을 알아볼 수 있도록 표시해야 합니다. routerLinkActive 디렉티브를 사용해 사용자가 클릭해 활성화 한 하이퍼링크 요소에 활성화 클래스를 추가할 수 있습니다. routerLink 디렉티브와 마찬가지로 속성 바인딩 할 수 있으며, 속성 바인딩 시에는 배열을 값으로 설정해야 합니다.

{% code-tabs %}
{% code-tabs-item title="app.component.html" %}
```markup
<nav>
  <ul class="nav justify-content-center">
    <li class="nav-item">
      <a 
        class="nav-link" 
        routerLink="home" 
        routerLinkActive="active">홈</a> 
    </li>
    <li class="nav-item">
      <a 
        class="nav-link" 
        [routerLink]="['search']" 
        [routerLinkActive]="['active']">검색</a>
    </li>
  </ul>
</nav>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### 프로그래밍 방식 내비게이션

`Router` 서비스를 컴포넌트에 주입, `navigate()` 메서드를 사용해 프로그래밍 방식으로 내비게이션 할 수 있습니다.

{% code-tabs %}
{% code-tabs-item title="app-nav.component.ts" %}
```typescript
import { Component } from '@angular/core';
import { Router } from '@angular/router';

@Component({
  selector: 'app-nav',
  template: `
    <nav>
      <ul class="nav justify-content-center">
        <li class="nav-item">
          <a 
            class="nav-link"
            (click)="goHome()"
            routerLinkActive="active">홈</a> 
        </li>
        <li class="nav-item">
          <a 
            class="nav-link" 
            (click)="goSearch()"
            routerLinkActive="active">검색</a>
        </li>
      </ul>
    </nav>
  `
})
export class AppNavComponent {

  constructor(private router:Router) {}
  
  goHome():void { this.router.navigate(['home']); }
  
  goSearch():void { this.router.navigate(['search']); }
  
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% hint style="info" %}
navigate\(\) 메서드에 배열 객체를 전달하는 이유는 서브 패스 라우팅 시, 다음과 같이 구성하기 때문입니다.

```typescript
// https://your-service.io/search/boo/woo
this.router.navigate(['search', 'boo', 'woo'])
```
{% endhint %}

