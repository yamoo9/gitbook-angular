# HttpClient 모듈

### HTTPClientModule 임포트

Angular 프레임워크 컴포넌트 또는 서비스에서 비동기 통신 하려면 [HttpClientModule](https://angular.io/api/common/http/HttpClientModule)을 `app.module.ts`에 불러와 `@NgModule`에 임포트 합니다.

{% code-tabs %}
{% code-tabs-item title="app.module.ts" %}
```typescript
import { HttpClientModule } from '@angular/common/http';

@NgModule({
  // ...
  imports: [
    // ...
    HttpClientModule
  ],
  // ...
})
export class AppModule {}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### HTTPClient 임포트

Angular 서비스 또는 컴포넌트에 [HttpClient](https://angular.io/api/common/http/HttpClient) 모듈을 불러온 후, 의존성 주입\([DI](https://angular.io/guide/dependency-injection), Dependency Injection\) 합니다.

{% code-tabs %}
{% code-tabs-item title="colors.service.ts" %}
```typescript
import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';

@Injectable({
  provideIn: 'root'
})
exprt class ColorsService {
  // 의존성 모듈 주입
  constructor( private http:HttpClient ) {}
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### 컴포넌트가 아닌, 서비스에 HttpClient를 사용하는 이유

개별 컴포넌트 마다 직접 HTTP 통신 요청을 하면 관리하거나, 테스트 하기 어려워 집니다. 반면 서비스를 사용해 HTTP 통신 과정을 캡슐화 하여 사용하면 관리하기가 매우 용이하기 때문입니다.

