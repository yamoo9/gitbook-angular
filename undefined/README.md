# 커스텀 디렉티브

Angular는 개발에 꼭 필요한 디렉티브 만을 제공하고 있습니다. 만약 개발에 필요한 디렉티브를 직접 제작하여 사용하고자 한다면 다음과 같이 작성합니다.

디렉티브 클래스는 `@Directive` 데코레이터를 사용해 정의합니다. 그리고 디렉티브 속성이 설정된 DOM 요소는 `ElementRef` 인스턴스의 `nativeElement` 속성을 통해 접근 조작 할 수 있습니다.

{% code-tabs %}
{% code-tabs-item title="app/hilight.directive.ts" %}
```typescript
import { Directive, ElementRef } from "@angular/core";

@Directive({
  selector: '[data-hilight]' // 속성 디렉티브 설정
})
export class HilightDirective {
  constructor(private _el:ElementRef) {
    this._el.nativeElement.style.cssText = `
      background: #ff0;
      color: #000;
      font-weight: 900;
    `;
  }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

직접 생성한 디렉티브를 컴포넌트에서 사용하려면 `@NgModule` 선언\(Declarations\) 항목에 추가 해야 합니다.

{% code-tabs %}
{% code-tabs-item title="app/app.module.ts" %}
```typescript
import { HilightDirective } from './hilight.directive';

@NgModule({
  declarations: [
    ...
    HilightDirective
  ],
  ...
});
```
{% endcode-tabs-item %}
{% endcode-tabs %}

디렉티브 등록을 마쳤으면 컴포넌트 템플릿에서 등록된 디렉티브를 사용할 수 있습니다.

{% code-tabs %}
{% code-tabs-item title="app/app.component.html" %}
```markup
<p>일반 텍스트</p>
<p data-hilight>하이라이트 디렉티브가 설정된 텍스트</p>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

