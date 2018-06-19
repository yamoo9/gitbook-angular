# 제너레이트 서비스

### Angular CLI를 통해 서비스 생성

Angular CLI 커멘드를 사용해 Service 기본 코드를 자동 생성할 수 있습니다.

{% code-tabs %}
{% code-tabs-item title="Angular CLI 명령어" %}
```bash
# ng generate service <서비스-이름>
$ ng g s <서비스-이름>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

자동 생성된 서비스 코드는 다음과 같습니다. 가만보면 앞서 다룬 코드와 다소 다른 것을 살펴볼 수 있는데요. `provideIn: 'root'` 코드가 생소합니다.

{% code-tabs %}
{% code-tabs-item title="popcorn.service.ts" %}
```typescript
import { Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root'
})
export class PopcornService {

  constructor() { }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Angular 6 부터 추가된 데코레이터 메타데이터 속성 `provideIn`은 애플리케이션 루트에 서비스를 공급하도록 설정하는 것입니다. 이와 같이 서비스에 서비스 공급 설정을 하면 기존에 작성하던 코드를 더 이상 추가하지 않아도 됩니다. 

### Angular 이전 버전 서비스 공급

Angular 5 버전까지는 앱 루트 모듈 또는 컴포넌트에 직접 서비스를 공급해 사용했습니다.

앱 루트모듈에 서비스를 공급하는 경우:

{% code-tabs %}
{% code-tabs-item title="app.module.ts" %}
```typescript
import { PopcornService } from './popcorn.service';

@NgModule({
  ...
  providers: [
    PopcornService
  ],
  ...
});
```
{% endcode-tabs-item %}
{% endcode-tabs %}

컴포넌트에 직접 서비스를 공급하는 경우:

```typescript
import { PopcornService } from './popcorn.service';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css'],
  provides: [PopcornService]
})
export class AppComponent {
  
}
```

