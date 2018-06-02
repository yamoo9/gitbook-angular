# 구조 디렉티브 사용 시, 주의점

Angular 구조 디렉티브를 사용해 데이터 순환과 조건 처리를 동시에 수행하고 싶을 수도 있을 겁니다.

{% code-tabs %}
{% code-tabs-item title="app/app.component.ts" %}
```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'recipes-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent {

  // 홀수 여부
  is_odd:boolean = true;
  // 숫자 데이터
  numbers:number[] = [1, 2, 3, 4, 5];

  // 홀짝 숫자 데이터 토글 메서드
  private toggleOddEvenNumbers() {
    this.is_odd = !this.is_odd;
  }
  
}

```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="app.component.html" %}
```markup
<div class="container">
  <div class="row">
    <div class="col-xs-12 col-md-3">
      <button 
        class="btn btn-primary" 
        (click)="toggleOddEvenNumbers()">홀/짝 숫자 토글</button>
      <ul class="list-group">
        <li class="list-group-item" 
            *ngFor="let number of numbers; let odd = odd" 
            *ngIf="is_odd === odd">
          {{number}}
        </li>
      </ul>
    </div>
  </div>
</div>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

하지만 안타깝게도 Angular 디렉티브를 하나 이상 요소에 사용할 경우 템플릿 해석 오류가 발생합니다. 오직 하나의 디렉티브 만을 사용하길 경고합니다. 콘솔에는 다음과 같은 오류 메시지가 출력됩니다. 

{% code-tabs %}
{% code-tabs-item title="Console 패널" %}
```typescript
compiler.js:215 Uncaught Error: Template parse errors:
Can't have multiple template bindings on one element. 
Use only one attribute prefixed with * ("odd = odd"> -->
  <li 
    class="list-group-item" 
    *ngFor="let number of numbers; let odd = odd" 
    [ERROR ->]*ngIf="is_odd === odd">
    {{number}}
  </li>
"): ng:///AppModule/AppComponent.html@6:84
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% hint style="info" %}
**NOTE.**  
구조 + 속성 디렉티브는 동시에 사용 가능합니다.
{% endhint %}

한 요소에 2개의 구조 디렉티브를 동시에 사용할 수 없기에 2개의 요소에 각각 디렉티브를 사용할 수 밖에 없습니다. 하지만 `<ul>` 요소에는 반드시 `<li>` 요소 만을 사용해야 하므로 `<li>` 요소 안에 `<li>` 요소를 사용할 수 없습니다. 웹 표준을 준수하면서 문제를 해결하려면 화면에 출력되지 않는 `<ng-container>` 요소를 사용해 그룹을 묶어 순환 처리하고, 그룹에 포함된 `<li>` 요소에서 조건 처리하면 됩니다.

{% code-tabs %}
{% code-tabs-item title="app.component.html" %}
```markup
<div class="container">
  <div class="row">
    <div class="col-xs-12 col-md-3">
      <button 
        class="btn btn-primary" 
        (click)="toggleOddEvenNumbers()">홀/짝 숫자 토글</button>
      <ul class="list-group">
        <!-- *ngFor 디렉티브 -->
        <ng-container *ngFor="let number of numbers; let odd = odd">
          <!-- *ngIf 디렉티브 -->
          <li class="list-group-item" *ngIf="is_odd === odd">
            {{number}}
          </li>
        </ng-container>
      </ul>
    </div>
  </div>
</div>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

