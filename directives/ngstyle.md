# \[ngStyle\] 디렉티브

Angular 애플리케이션 제작 시, 인라인 스타일을 동적으로 설정하려면 `[ngStyle]` 디렉티브를 사용합니다. 버튼 컴포넌트의 활성/비활성 상태에 따라 배경 색상을 변경하는 예제를 살펴보겠습니다.

{% code-tabs %}
{% code-tabs-item title="app/button/button.component.ts" %}
```typescript
import { Component } from "@angular/core";

@Component({...})
export class ButtonComponent {

  public content:string;
  public is_disabled:boolean;

  // 컴포넌트 생성 과정에서 속성 값 초기화
  constructor() {
    this.is_disabled = Math.random() > 0.5 ? true : false;
    this.content = this.is_disabled ? '활성' : '비활성';
  }

  // is_disabled 상태에 딸 설정할 컬러 값을 반환하는 메서드
  public assignBgColor(): string {
    return this.is_disabled ? '#6c5ce7' : '#b2bec3';
  }

}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

`[ngStyle]` 속성 디렉티브에 설정되는 값은 TypeScript 식이 사용됩니다. 객체\(`{}`\) 내부에 속성 `'background-color'` 값으로 `assignBgColor()` 컴포넌트 메서드를 실행한 후 결과 값을 받아 설정합니다.

{% code-tabs %}
{% code-tabs-item title="app/button/button.component.html" %}
```markup
<button
  type="button"
  [disabled]="is_disabled"
  [ngStyle]="{'background-color': assignBgColor()}"
>{{ content }}</button>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% hint style="info" %}
**NOTE.**   
`'background-color'` 대신 `backgroundColor` 속성 값을 사용할 수도 있습니다.
{% endhint %}

