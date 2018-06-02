# Renderer2 활용해 디렉티브 개선

_Renderer2_ 클래스를 활용하면 직접 DOM을 조작하지 않고도 애플리케이션 요소를 조작 할 수 있습니다. 장점은 DOM에 직접 접근할 수 없는 환경에서 렌더링 할 수 있는 애플리케이션 개발이 보다 쉬워진다는 점입니다.

{% hint style="info" %}
**NOTE.**  
Renderer 는 Renderer2 이후 사용이 권장되지 않습니다.
{% endhint %}

Renderer2 클래스를 활용하는 간단한 커스텀 디렉티브를 생성해보겠습니다.

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

