# 사용자 속성 제어

디렉티브를 재사용 하려면 사용하는 외부 환경에서 컨트롤 할 속성 값을 전달해야 합니다. 사용자가 디렉티브에 속성 값을 전달해 디렉티브 내부에서 그 값을 처리하게 하는 것이죠. 디렉티브 속성이 설정된 요소는 컴포넌트 이기도 하니 앞서 공부 했던 컴포넌트 통신 방법을 사용하면 디렉티브에 속성을 전달할 수 있습니다. Input 데코레이터를 활용하면 되겠죠?

{% code-tabs %}
{% code-tabs-item title="app/directives/rainbow.directive.ts" %}
```typescript
import { Directive, HostBinding, HostListener, Input } from '@angular/core';

@Directive({ selector: '[data-rainbow]' })
export class RainbowDirective {

  // 외부에서 colors 값 전달 받음 (기본 값 설정)
  @Input() colors:string[] = [
    'darksalmon', 
    'hotpink', 
    'lightskyblue', 
    'goldenrod', 
    'peachpuff', 
    'mediumspringgreen', 
    'cornflowerblue', 
    'blanchedalmond', 
    'lightslategrey'
  ];
  
  @HostBinding('style.color') color:string;
  @HostBinding('style.border-color') borderColor:string;
  
  @HostListener('keydown') newColor() {
    const pick = Math.floor(Math.random() * this.colors.length);
    this.color = this.borderColor = this.colors[pick];
  }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

디렉티브 속성이 적용된 요소에 colors 속성 바인딩 하여 사용자가 특정 값을 전달할 수 있습니다.

{% code-tabs %}
{% code-tabs-item title="app/app.component.html" %}
```markup
<input 
  type="text" 
  data-rainbow
  [colors]="['#778beb', '#f5cd79', '#ea8685', '#303952', '#3dc1d3']">
```
{% endcode-tabs-item %}
{% endcode-tabs %}

