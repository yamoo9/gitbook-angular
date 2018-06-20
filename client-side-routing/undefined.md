# 매개변수 라우트

### 매개변수 라우트

때로는 패스의 일부가 변수가 되어야 하는 경우가 많습니다. 일반적인 예로 ID를 들 수 있습니다. 뉴스 또는 세미나의 특정 ID 값에 따른 페이지를 URL로 구성한다면 다음과 같을 것입니다.

```typescript
https://your-service.io/news/7
https://your-service.io/seminar/yamoo9
```

각 패스에 설정된 ID 값에 따라 컴포넌트를 연결하는 라우트를 설정하는 코드는 다음과 같을 겁니다. 하지만 이와 같은 방법은 무수히 많은 ID 값을 처리하기에 매우 비 효율적 입니다.

{% code-tabs %}
{% code-tabs-item title="app.module.ts" %}
```typescript
const routes:Routes = [
  // ...
  { path: 'news/7', component: News7Component, },
  // ...
  { path: 'seminar/yamoo9', component: SeminarYamoo9Component, },
  // ...
];
```
{% endcode-tabs-item %}
{% endcode-tabs %}

보다 나은 해결책은 하나의 컴포넌트에 ID를 변수로 전달하는 방법입니다. 즉, URL 패스에 ID를 전달하면 이를 컴포넌트는 변수로 받아 처리하는 것입니다. 이와 같은 방법을 매개변수 라우팅 이라고 부릅니다. 콜론\(`:`\)으로 설정된 이름은 컴포넌트에서 변수로 사용할 수 있습니다.

{% code-tabs %}
{% code-tabs-item title="app.module.ts" %}
```typescript
const routes:Routes = [
  { path: 'news/:id', component: NewsComponent },
  { path: 'seminar/:speaker', component: SeminarComponent },
];
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% hint style="info" %}
매개변수가 설정된 패스는 일반 패스보다 우선 적용됩니다. 예를 들어 아래와 같이 설정되어 있을 경우, `search/tissue` 패스는 SearchComponent를 아웃렛\(Outlet\) 합니다.

```typescript
const routes:Routes = [
  { path: 'search/tissue', TissueComponent },
  { path: 'search/:keyword', SearchComponent }, // 우선
];
```
{% endhint %}

### 활성화된 라우트

라우트 설정을 통해 패스에 매개변수 값을 전달했다면, 그 값을 컴포넌트에서 받을 수 있어야 합니다. 컴포넌트에서 매개변수에 설정된 인자 값을 받기 위해서 ActiveatedRoute 서비스를 컴포넌트에 주입해 사용해야 합니다.

{% code-tabs %}
{% code-tabs-item title="search.component.ts" %}
```typescript
// ActivatedRoute 모듈 로드
import { ActivatedRoute } from '@angular/router';
import { Component, OnInit } from '@angular/core';

@Component({...})
export class SearchComponent implements OnInit {
  
  // ActivatedRoute 서비스 주입
  constructor(private route:ActivatedRoute) {}
  
  ngOnInit():void {
    // params <Observable> 객체의 
    // subscribe() 메서드를 통해params 객체 출력
    this.route.params.subscribe( params => console.log(params));
  }
  
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

`search/worldcup`으로 URL을 변경 접속하면 콘솔 패널에 다음과 같이 출력되는 것을 확인할 수 있습니다.

{% code-tabs %}
{% code-tabs-item title="Console" %}
```typescript
{ keyword: 'worldcup' }
```
{% endcode-tabs-item %}
{% endcode-tabs %}

이와 같은 설정으로 `검색/키워드` 형태의 URL은 모두 SearchComponent를 화면에 렌더링하고, 키워드 또한 `params` 값으로 잘 받아옵니다. 하지만 문제가 발생했습니다. `검색` URL로 접속하면 SearchComponent를 화면에 렌더링 하지 않습니다. URL이 일치하지 않기 때문입니다.

이 문제를 해결하려면 다음과 같이 `검색`, `검색/키워드` 형태의 패스를 모두 설정해야 합니다.

{% code-tabs %}
{% code-tabs-item title="app.module.ts" %}
```typescript
const routes:Routes = [
  { path: 'search', component: SearchComponent },
  { path: 'search:keyword', component: SearchComponent },
];
```
{% endcode-tabs-item %}
{% endcode-tabs %}

매개변수 전달 과정을 살펴봤으니, 이어서 전달 받은 매개 변수 `keyword`를 토대로 검색을 수행하는 코드를 작성해 실제 검색이 수행되도록 할 수 있습니다.

{% code-tabs %}
{% code-tabs-item title="search.component.ts" %}
```typescript
export class SearchComponent implements OnInit {
  
  constructor(private route:ActivatedRoute) {}
  
  ngOnInit():void {
    this.route.params.subscribe( params => this.search(params['keyword']));
  }
  
  search(keyword:string):void {
    // 전달 받은 키워드로 검색 수행
  }
  
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### URL 업데이트

현재 작성된 로직 만으로는 검색 수행 결과가 화면에 정상 출력되지만, URL 까지 변경 되지는 않습니다. 검색 키워드 변경에 따른 URL, 검색 처리를 동시에 업데이트 하려면 search 메서드를 다음과 같이 변경합니다.

```typescript
// Router 호출
import { Router, ActivatedRoute } from '@angular/router';

@Component({...})
export class SearchComponent implements OnInit {
  
  constructor(
    private route:ActivatedRoute,
    // Router 주입
    private router:Router
  ) {}
  
  ngOnInit():void {
    this.route.params.subscribe(params => this.search(params['keyword']));
  }
  
  onSearch(keyword:string):void {
    // 키워드 입력 후, 검색 버튼을 누르면 URL 업데이트
    this.router.navigate(['search', keyword]);
  }
    
  search(keyword:string):void {
    // 전달 받은 키워드로 검색 수행
  }
}


```

### 선택적 매개변수

`'search'` 패스에 설정된 컴포넌트가 동일 함에도, `keyword` 식별 값에 따른 별도의 패스를 설정 했었습니다. 뭔가 불필요한 공정처럼 느껴졌는데, 다행히 Angular는 선택적으로 매개변수를 처리하는 메커니즘을 제공하고 있습니다.

{% code-tabs %}
{% code-tabs-item title="app.module.ts" %}
```typescript
const routes:Routes = [
  { path: 'search', component: SearchComponent },
  { path: 'search:keyword', component: SearchComponent },
];
```
{% endcode-tabs-item %}
{% endcode-tabs %}

먼저 수행할 일은 기존의 `search:keyword` 패스를 제거하는 것입니다.

{% code-tabs %}
{% code-tabs-item title="app.module.ts" %}
```typescript
const routes:Routes = [
  { path: 'search', component: SearchComponent },
];
```
{% endcode-tabs-item %}
{% endcode-tabs %}

이어서 onSearch\(\) 메서드를 통해 고정된 패스로 내비게이션 되는 대신, 매개 변수를 포함한 객체를 전달합니다.

{% code-tabs %}
{% code-tabs-item title="search.component.ts" %}
```typescript
onSearch(keyword:string):void {
  // Angular의 선택적 매개변수 전달 방법
  this.router.navigate(['search', {keyword: keyword}]);
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

이전 설정의 패스는 `/search/pepsi` 이었지만,  설정을 변경한 패스는 `/search;keyword=pepsi`로 바뀝니다. 남은 일은 키워드가 전달되지 않은 경우의 대비를 코드에 반영하는 것입니다. 즉, 키워드가 존재할 때만 검색을 수행합니다.

{% code-tabs %}
{% code-tabs-item title="search.component.ts" %}
```typescript
ngOnInit():void {
    this.route.params.subscribe(params => {
      let keyword = params['keyword'];
      if ( keyword ) {
        this.search(params['keyword']);
      } 
    });
  }
```
{% endcode-tabs-item %}
{% endcode-tabs %}



