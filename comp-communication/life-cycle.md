# 컴포넌트 라이프사이클

Angular는 컴포넌트 라이프 사이클 훅을 통해 특정 시점에 동작을 실행 시킵니다. 제공되는 라이프 사이클 훅은 총 8가지 입니다.

| ngOnChanges | 데이터 바인딩 된 인풋 속성이 변경 될 때 마다 호출됩니다. \(성능 문제로 가급적 제한 사용 권장\) |
| --- | --- | --- | --- | --- | --- | --- | --- |
| ngOnInit | 컴포넌트 초기화 시, 1회 호출됩니다. |
| ngDoCheck | 모든 변경 사항을 감지하여 호출됩니다. \(성능 문제 주의\) |
| ngAfterContentInit | 콘텐츠\(ng-content 등\)가 추가된 이후 호출됩니다. |
| ngAfterContentChecked | 콘텐츠 내용 체크 후, 호출됩니다. |
| ngAfterViewInit | 컴포넌트 뷰\(자식 컴포넌트 뷰 포함\) 초기화 후 호출됩니다. |
| ngAfterViewChecked | 컴포넌트 뷰\(자식 컴포넌트 뷰 포함\) 체크 후, 호출됩니다. |
| ngOnDestroy | 컴포넌트가 파괴 되었을 때 1회 호출됩니다. |

### ngOnInit 라이프 사이클 훅

가장 자주 사용 되는 `ngOnInit` 훅 예제를 살펴봅시다. 컴포넌트가 만들어 질 때 처리해야 할 일이 많을 경우, `constructor` 대신 `ngOnInit` 훅을 사용하는 것이 좋습니다. 다른 라이프 사이클 훅도 사용법이 동일합니다.

{% code-tabs %}
{% code-tabs-item title="app/app.component.ts" %}
```typescript
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'my-app',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent implements OnInit {
  constructor() {}

  // 라이프 사이클 훅
  ngOnInit() {
    // 컴포넌트 초기화 시, 처리할 일 호출
    this.setupData();
    this.doStuff();
    // ...
  }

  setupData() {}
  doStuff() {}
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### 멀티 라이프 사이클 훅

여러 개의 라이프 사이클 훅을 사용하는 방법도 간단합니다.

{% code-tabs %}
{% code-tabs-item title="app/app.component.ts" %}
```typescript
import { Component, OnInit, OnDestroy } from '@angular/core';

@Component({
  selector: 'my-app',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent implements OnInit, OnDestroy {

  constructor() {}

  ngOnInit() {
    console.log('컴포넌트 초기화 시 실행');
  }

  ngOnDestroy() {
    console.log('컴포넌트 파괴 시 실행');
  }
  
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### ngOnChanges 라이프 사이클 훅

다음과 같은 컴포넌트가 있다고 가정해봅니다. 부모 컴포넌트가 자식 컴포넌트에 속성 바인딩 방식으로 데이터를 전달합니다.

{% code-tabs %}
{% code-tabs-item title="app/my-todos/my-todos.component.html" %}
```typescript
<my-todo [title]="title" [content]="content"></my-todo>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

예를 들어 `title` 속성이 변경될 때 특정 일을 수행하고자 한다면 `ngOnChange()` 라이프 사이클 훅 메서드에서 `title` 속성 값이 변경 됨을 감지하여 무언가 처리할 수 있습니다.

{% code-tabs %}
{% code-tabs-item title="app/my-todo/my-todo.component.ts" %}
```typescript
import { Component, Input, SimpleChanges, OnChanges } from '@angular/core';

@Component({
  // ...
})
export class MyTodoComponent implements OnChanges {
  @Input() title: string;
  @Input() content: string;

  constructor() { }

  ngOnChanges(changes: SimpleChanges) {
    for (let property in changes) {
      if (property === 'title') {
        console.log('이전 상태:', changes[property].previousValue);
        console.log('현재 상태:', changes[property].currentValue);
      }
    }
  }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

