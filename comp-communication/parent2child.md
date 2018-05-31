# 부모 컴포넌트 ➡ 자식 컴포넌트

컴포넌트와 중첩된 컴포넌트 사이에 데이터를 공유하는 과정에 대해 학습해보겠습니다. 부모 컴포넌트는 데이터를 가지고 있고, 자식 컴포넌트는 부모 컴포넌트로부터 데이터를 전달 받아 템플릿을 통해 뷰를 구현해야 합니다.

### 부모 컴포넌트 코드

부모 컴포넌트는 `foods` 데이터를 가지고 있고, 템플릿에서 `<app-child>` 자식 컴포넌트를 사용하고 있습니다. 자신이 가진 `foods` 데이터를 `*ngFor` 디렉티브를 사용해 순환한 후, 커스텀 속성 `[element]`을 사용해 자식 컴포넌트에 데이터를 전달합니다.

```typescript
// app/parent/parent.component.ts

import { Component } from "@angular/core";

@Component(metadata)
export class ParentComponent {

  // 부모가 가진 데이터
  public foods:object[] = [
    {
      type: '중식',
      name: '짜장면',
      content: '달콤한 짜장 소스에 면을 버무려 먹으면 참 맛있어요!'
    }
  ];

}
```

```markup
<!-- app/parent/parent.component.html -->

<!-- food 값을 [element] 속성에 전달하므로 자식 컴포넌트에 전달  -->
<app-child *ngFor="let food of foods" [element]="food"></app-child>
```

### 자식 컴포넌트 코드

자식 컴포넌트는 부모로 부터 전달 받은 데이터 `element`를 컴포넌트 클래스 속성으로 설정해야 합니다. 이 때 자식 컴포넌트는 [`Input`](https://angular.io/api/core/Input) 모듈을 불러와 `@Input()` 데코레이터를 사용해 `element` 속성을 설정해야 부모 컴포넌트의 데이터를 받아 올 수 있습니다.

```typescript
// app/child/child.component.ts

import { Component, OnInput, Input } from "@angular/core";

@Component(metadata)
export class ChildComponent {

  // @Input() 데코레이터를 통해 부모 컴포넌트의 데이터를 전달 받음
  @Input()
  element: {type:string, name:string, content:string};

  constructor(){}
  onInput(){}
}
```

```markup
<!-- app/child/child.component.html -->

<!-- 부모 컴포넌트로부터 전달 받은 element를 사용해 데이터 바인딩 -->
<li class="list-group-item">
  <h4>{{ element.name }}</h4>
  <p [ngSwitch]="element.type">
    <strong *ngSwitchCase="'중식'">{{element.content}}</strong>
    <em *ngSwitchDefault>{{ element.content }}</em>
  </p>
</li>
```

## 커스텀 속성 별칭\(Alias\)

부모 컴포넌트가 전달한 속성 값의 이름과 자식 컴포넌트에서 전달 받는 속성 이름이 다를 경우, 별칭을 사용해 부모 컴포넌트가 전달한 값을 자식 컴포넌트가 이해하게 만들 수 있습니다.

부모 컴포넌트 템플릿 코드:

```markup
<!-- app/parent/parent.component.html -->

<!-- [food]를 사용하여 자식 컴포넌트에 데이터를 전달 -->
<app-child *ngFor="let food of foods" [food]="food"></app-child>
```

자식 컴포넌트 `@Input()` 데코레이터에 `'부모가 전달한 속성 별칭'`을 설정하면 자식 컴포넌트가 정상 작동됩니다.  
 \(`food` ⇒ `element` 설정\)

자식 컴포넌트 코드:

```typescript
// app/child/child.component.ts

import { Component, OnInput, Input } from "@angular/core";

@Component(metadata)
export class ChildComponent {

  // 부모 컴포넌트 템플릿에서 커스텀 속성 바인딩한 `food` 값을
  // @Input() 데코레이터에 설정하여 별칭으로 사용
  @Input('food')
  element: {type:string, name:string, content:string};

  constructor(){}
  onInput(){}
}
```

