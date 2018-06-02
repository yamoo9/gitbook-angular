# 커스텀 구조 디렉티브

앞서 다룬 사용자 정의 속성 디렉티브 외에도 `*ngIf`, `*ngFor`와 같은 구조 디렉티브를 사용자 정의할 수 있습니다. if 조건의 반대인 unless 디렉티브를 생성해보겠습니다. 구조 디렉티브를 생성 하려면 `ViewContainerRef`, `TemplateRef`, `Input` 클래스를 불러 와야 합니다. 제작 방법은 아래 코드를 참고하세요.

{% code-tabs %}
{% code-tabs-item title="app/directives/unless.directive.ts" %}
```typescript
import { Directive, TemplateRef, ViewContainerRef, Input } from '@angular/core';

@Directive({selector: 'ngUnless'})
export class UnlessDirective {
  // selector 값과 이름이 동일
  @Input() set ngUnless(condition:boolean) {
    // 전달된 조건 값이 거짓이면
    if (!condition) {
      // 뷰컨테이너 참조를 통해 템플릿 생성 포함
      this.vc.createEmbededView(this.templ);
    } else {
      // 뷰컨테이너 참조를 통해 클리어
      this.vc.clear();
    }
  }
  constructor(private templ:TemplateRef<any>, vc:ViewContainerRef){}
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

아래 인용문 템플릿은 조건이 `false`이므로 화면에 구현됩니다. 조건 값이 `true`였다면 아무것도 화면에 그려지지 않습니다. 즉, `*ngIf`과 정반대로 구현이 됩니다.

{% code-tabs %}
{% code-tabs-item title="app/app.component.html" %}
```markup
<blockquote lang="en" cite="https://goo.gl/zPNvGS" *ngUnless="false">
  <p>unless we are willing to die for it.</p>
  <cite>che Guevara</cite>
</blockquote>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

