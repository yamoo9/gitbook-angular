# ViewChild 데코레이터

[ViewChild](https://angular.io/api/core/ViewChild) 데코레이터를 사용하면 자식 컴포넌트 또는 DOM에 접근할 수 있습니다. ViewChild는 컴포넌트, 디렉티브 또는 템플릿 참조 선택자와 일치하는 첫번째 요소를 반환합니다. ViewChild의 장점은 동적으로 참조가 새로운 요소로 변경되면 자동으로 업데이트 되어 관리된다는 점입니다.

> **NOTE.**  
>  자식들\(Children\)에 접근하려면 ViewChildren을 사용합니다.

## DOM 요소에 접근

템플릿 레퍼런스 변수가 설정된 기본 DOM 요소에 접근할 수 있습니다. 템플릿에 `#pizzaToping` 참조 변수가 있다고 합시다.

```markup
<div class="form-group">
  <label for="pizza-toping">피자 토핑</label>
  <input
    #pizzaToping
    type="text"
    class="form-control"
    name="pizza-toping"
    id="pizza-toping"
    aria-describedby="pizza-toping-desc"
    placeholder="좋아하는 피자 토핑 입력">
  <span id="pizza-toping-desc" class="form-text text-muted">좋아하는 피자 토핑을 입력해주세요.</span>
</div>
```

ViewChild, ElementRef 모듈을 불러와 ViewChild 데코레이터를 사용해 템플릿 참조 변수 `#pizzaToping`를 설정하면 DOM 요소에 접근할 수 있습니다.

```typescript
import { Component, AfterViewInit, ViewChild, ElementRef } from "@angular/core";

@Component({ ... })
export class AppComponent implements AfterViewInit {

  @ViewChild('pizzaToping') pizzaToping: ElementRef;

  ngAfterViewInit() {
    // ElementRef의 nativeElement 속성을 통해
    // DOM 객체 접근 가능
    this.pizzaToping.nativeElement.value = '앤쵸비! 🍕🍕';
  }
}
```

## 자식 컴포넌트에 접근

부모 컴포넌트에서 자식 컴포넌트 멤버\(속성, 메서드 등\)에 접근할 수도 있습니다. 먼저 자식 컴포넌트를 불러온 후, ViewChild 데코레이터에 설정한 후, 이를 통해 접근 가능합니다.

```typescript
import {
  Component,
  ViewChild,
  AfterViewInit } from "@angular/core";

import { ChildComponent } from './child/child.component';

@Component({ ... })
export class AppComponent implements AfterViewInit {

  @ViewChild(ChildComponent) child: ChildComponent;

  ngAfterViewInit() {
    console.log(this.child.whoAmI()); // "👶 자식 컴포넌트입니다."
  }
}
```

