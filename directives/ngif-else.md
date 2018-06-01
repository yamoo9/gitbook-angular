# \*ngIf - else 디렉티브

## \*ngIf 디렉티브

`*ngIf` 디렉티브는 화면에 렌더링되는 과정에서 DOM에서 제외됩니다. 즉, 실제로 존재하지 않는 것입니다. 디렉티브 속성 값으로 설정된 데이터 유형 값이 `true`일 경우 화면에 그려지며, `false`일 경우는 그려지지 않습니다. 즉, if문과 마찬가지로 조건 값이 참일 경우와 거짓일 경우를 구분하여 처리됩니다.

{% code-tabs %}
{% code-tabs-item title="app/button/button.component.ts" %}
```typescript
import { Component } from "@angular/core";

...

@Component(metadata)
export class ButtonComponent {

  // 값이 거짓일 경우, 화면에 렌더링되지 않습니다.
  public is_renderting:boolean = false;

  // 값을 전달 받아, 화면에 표시 또는 비표시 설정하는 메서드
  public chageRenderingState(value: boolean): void {
    this.is_renderting = value;
  }

  // 화면 표시, 비표시를 토글하는 메서드
  public toggleRenderingState(): void {
    this.is_renderting = !this.is_renderting;
  }

}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="app/button/button.component.html" %}
```markup
<div class="button-group" role="group">
  <button type="button" (click)="chageRenderingState(true)">추가</button>
  <button type="button" (click)="chageRenderingState(false)">제거</button>
  <button type="button" (click)="toggleRenderingState()">토글</button>
</div>

<p *ngIf="is_renderting">*ngIf 디렉티브에 의해 화면에 렌더링 될지, 아닐지가 결정됩니다.</p>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

`*ngIf` 디렉티브는 내부적으로 다음과 같이 처리됩니다. `[ngIf]` 속성 바인딩과 `<ng-template>`를 사용해 화면에 그림을 그릴지, 그리지 않을지를 결정하게 되는 것입니다. 문법이 다소 복잡하게 느껴지는 반면, `*ngIf` 디렉티브를 활용하면 쉽게 사용할 수 있습니다.

```markup
<ng-template [ngIf]="is_renderting">
  <p>*ngIf 디렉티브에 설정된 값에 의해 화면에 렌더링 될지, 아닐지가 결정됩니다.</p>
</ng-template>
```

{% hint style="info" %}
**NOTE.**    
`<ng-template>`는 화면에 표시되지 않는 템플릿 요소입니다.
{% endhint %}

## else / ng-template

Angular는 `*ngIf` 디렉티브는 제공하는 반면, `else`에 대한 디렉티브 대신 다음과 같이 구문으로 처리하는 방식을 제공합니다. 그리고 `<ng-template>` 요소를 사용하고 식별자 `#`를 설정해 사용합니다. \(다소 구문이 생소하고, 불편하지만 Angular 프레임워크 사용자로 익숙해져야 합니다.\)

```markup
<p *ngIf="is_renderting; else elseStatement">
  is_renderting 값이 참이면 화면에 렌더링 됩니다.
</p>
<ng-template #elseStatement>
  <p>is_renderting 값이 거짓이면 화면에 렌더링 됩니다.</p>
</ng-template>
```

혹은 다음과 같은 `then ~ else -` 방법으로 코드를 기술할 수도 있습니다.

```markup
<p *ngIf="is_renderting; then #ifStatement else elseStatement"></p>
<ng-template #ifStatement>is_renderting 값이 참이면 화면에 렌더링 됩니다.</ng-template>
<ng-template #elseStatement>is_renderting 값이 거짓이면 화면에 렌더링 됩니다.</ng-template>
```

## 화면에서 감추는 것이 아니라, 제거시키는 이유

화면에 보임/감춤 처리하는 별도의 디렉티브를 Angular는 제공하지 않습니다. 대신 아래와 같은 방법으로 화면에 보임/감춤 설정이 가능합니다.

```markup
<p [style.display]="'block'">
  style.display 값이 block으로 설정된 요소는 화면에 표시됩니다.
</p>
<p [style.display]="'none'">
  style.display 값이 none으로 설정된 요소는 화면에서 감춰집니다.
</p>
```

[Angular API 문서](https://angular.io/guide/structural-directives#why-remove-rather-than-hide)에 따르면 성능 이슈 문제로 감춤보다는 제거를 택한다고 안내합니다. 화면에서 감춰져도 컴포넌트는 일을 계속한다는 것입니다.

컴포넌트가 DOM을 지속적으로 관찰\(이벤트 리스닝\)하므로 Angular는 데이터 바인딩에 영향을 줄 수 있는 변경 사항을 계속 확인합니다. 화면에서 감춰질 뿐인 요소는 사용자에게 안 보이지만, 연결된 컴포넌트와 하위 컴포넌트는 리소스를 묶기 때문에 성능 및 메모리 부담이 상당한 성능 이슈를 일으킵니다.

물론, 감추는 것이 제거했다가 추가하는 것보다 빠릅니다. 컴포넌트에 이전 상태가 보존되어 있어 보여줄 준비가 되어 있기 때문입니다. 그리고 컴포넌트가 초기화되지 않는다는 장점도 있습니다. 컴포넌트를 다시 초기화하는 것은 비용이 많이 드는 작업입니다. 그런 이유로 보임/감춤이 때로는 옳은 일입니다.

하지만 지속적으로 보임/감춤 처리할 컴포넌트\(예: 토글\)가 아니라면, 감춤 보다는 DOM 요소를 제거하고, 사용하지 않는 리소스를 복구하는 것이 성능 상 이롭습니다.

