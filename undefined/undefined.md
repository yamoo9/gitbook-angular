# 제너레이트 디렉티브

컴포넌트 자동 생성 명령에서 살펴 봤듯이 디렉티브 또한 Angular CLI 명령을 사용해 자동 생성할 수 있습니다.

```bash
# ng generate directive <directives/디렉티브-이름>
$ ng g d <directives/디렉티브-이름>
```

명령이 실행되면 directives 디렉토리 내부에 `directive.ts` 파일이 자동 생성되고, `app.module.ts` 파일이 자동 업데이트 됩니다. 역시나 Angular CLI를 사용하니 지루하고, 반복되는 공정을 줄여주니 편리합니다. 

```bash
ng g d directives/hilight
CREATE src/app/directives/hilight.directive.ts (145 bytes)
UPDATE src/app/app.module.ts (606 bytes)
```

자동 생성된 코드를 살펴보면 커스텀 디렉티브를 구현하기 위한 코드가 준비되어 있습니다.

{% code-tabs %}
{% code-tabs-item title="app/directives/hilight.directive.ts" %}
```typescript
import { Directive } from '@angular/core';

@Directive({
  selector: '[appHilight]'
})
export class HilightDirective {

  constructor() { }

}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="app/app.module.ts" %}
```typescript
import { HilightDirective } from './directives/hilight.directive';

@NgModule({
  declarations: [
    ...,
    HilightDirective
  ],
  ...
});
```
{% endcode-tabs-item %}
{% endcode-tabs %}

