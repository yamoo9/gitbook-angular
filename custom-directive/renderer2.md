# Renderer2 활용

_Renderer2_ 클래스를 활용하면 직접 DOM을 조작하지 않고도 애플리케이션 요소를 조작 할 수 있습니다. 장점은 DOM에 직접 접근할 수 없는 환경에서 렌더링 할 수 있는 애플리케이션 개발이 보다 쉬워진다는 점입니다.

{% hint style="info" %}
**NOTE.**  
Renderer 는 Renderer2 이후 사용이 권장되지 않습니다.
{% endhint %}

Renderer2 클래스를 활용하는 간단한 커스텀 디렉티브를 생성해보겠습니다.

{% code-tabs %}
{% code-tabs-item title="app/directives/assign-phone.directive.ts" %}
```typescript
import { Directive, OnInit, ElementRef, Renderer2 } from '@angular/core';

@Directive({selector: '[data-assign-phone]'})
export class AssignPhoneDirective {
  
  constructor(private _el:ElementRef, private _renderer:Renderer2) {}
  
  ngOnInit(){
    this._renderer.addClass(_el.nativeElement, 'phone');
  }

}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

정의된 커스텀 디렉티브는 템플릿 요소에 속성을 추가하면 잘 작동합니다. 전반적으로 Renderer2 사용법이 DOM을 직접 조작하는 것보다 복잡하지 않은 것을 확인 수 있습니다.

{% code-tabs %}
{% code-tabs-item title="app/app.component.html" %}
```markup
<div data-assign-phone> phone 클래스를 적용하는 커스텀 디렉티브 </div>

<!-- 
  렌더링 결과:
  <div class="phone"> phone 클래스를 적용하는 커스텀 디렉티브 </div> 
-->
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### Renderer2 활용

Angular 애플리케이션 제작 시, Renderer2를 활용하면 DOM API와 유사한 메서드를 활용할 수 있습니다. 각 조작 방법을 살펴보겠습니다.

#### createElement / createText / appendChild

새로운 DOM 요소를 만들고 다른 요소 안에 추가할 수 있습니다. 사용법은 DOM 스크립트와 동일합니다.

{% code-tabs %}
{% code-tabs-item title="app/directives/renderer2.directive.ts" %}
```typescript
import { Directive, OnInit, ElementRef, Renderer2 } from '@angular/core';

@Directive({selector: '[data-renderer2]'})
export class Renderer2Directive implements OnInit {

  consructor(private _el:ElementRef, private _renderer:Renderer2) {}

  ngOnInit() {
    const r = this._renderer;
    const div = r.createElement('div');
    const text = r.createTextNode('커스텀 디렉티브 with Renderer2');
    r.appendChild(div, text);
    r.appendChild(this._el.nativeElement, div);
  }

}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

#### setAttribute / removeAttribute

DOM 요소의 속성을 추가하거나, 제거할 수 있습니다.

{% code-tabs %}
{% code-tabs-item title="app/directives/renderer2.directive.ts" %}
```typescript
consructor(private _el:ElementRef, private _renderer:Renderer2) {}

ngOnInit() {
  this._renderer.setAttribute(this._el.nativeElement, 'aria-hidden', false);
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

#### addClass / removeClass

jQuery 메서드와 유사하게 DOM 요소의 클래스 속성을 추가 하거나, 제거할 수 있습니다.

{% code-tabs %}
{% code-tabs-item title="app/directives/renderer2.directive.ts" %}
```typescript
consructor(private _el:ElementRef, private _renderer:Renderer2) {}

ngOnInit() {
  this._renderer.removeClass(this._el.nativeElement, 'phone');
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

#### setStyle / removeStyle

DOM 요소에 인라인 스타일을 설정하거나, 제거할 수 있습니다.

{% code-tabs %}
{% code-tabs-item title="app/directives/renderer2.directive.ts" %}
```typescript
consructor(private _el:ElementRef, private _renderer:Renderer2) {}

ngOnInit() {
  this._renderer.setStyle(this._el.nativeElement, 'border-left', '4px double #990');
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="app/directives/renderer2.directive.ts" %}
```typescript
consructor(private _el:ElementRef, private _renderer:Renderer2) {}

ngOnInit() {
  this._renderer.removeStyle(this._el.nativeElement, 'border-left');
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

#### setProperty

DOM 요소의 속성을 설정할 수 있습니다. title 속성을 설정하거나, value 값을 설정 할 수 있습니다.

{% code-tabs %}
{% code-tabs-item title="app/directives/renderer2.directive.ts" %}
```typescript
consructor(private _el:ElementRef, private _renderer:Renderer2) {}

ngOnInit() {
  this._renderer.setProperty(this._el.nativeElement, 'title', '새 창 열림');
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="app/directives/renderer2.directive.ts" %}
```typescript
consructor(private _el:ElementRef, private _renderer:Renderer2) {}

ngOnInit() {
  this._renderer.setProperty(this._el.nativeElement, 'value', '와이드 TV뷰');
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% hint style="info" %}
**NOTE.**  
Renderer2 클래스의 전체 메서드는 [Angular - Renderer2](https://angular.io/api/core/Renderer2) 에서 살펴보세요.
{% endhint %}



