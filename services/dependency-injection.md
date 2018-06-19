# 의존성 주입

Angular 서비스는 클래스로 생성 과정을 통해 서비스 객체를 생성할 수 있습니다만, 아래와 같이 사용하는 것은 권장되는 방법이 아닙니다. 서비스 객체를 컴포넌트 마다 생성해 사용하면 관리 및 테스트 하기 어렵기 때문입니다.

{% code-tabs %}
{% code-tabs-item title="app.component.ts" %}
```typescript
import { Component } from '@angular/core';

// 팝콘 서비스를 불러옵니다.
import { PopcornService } from './popcorn.service';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css'],
})
export class AppComponent {
  
  popcornService:PopcornService;
  
  constructor() {
    // 생성된 서비스 객체를 참조합니다.
    this.popcornService = new PopcornService();
  }
  
  cook(quantity:number):void { 
    console.log('팝콘', quantity, '통이 조리되었습니다.'); 
  }
  
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### 서비스 객체를 주입하는 방법

서비스 객체를 주입하는 방법은 `constructor`에 `private` 접근 제어자를 사용해 비공개 속성으로 선언합니다. 그리고 컴포넌트 데코레이터 메타데이터 값으로 `providers` 속성에 서비스 클래스를 공급해야 합니다.

{% code-tabs %}
{% code-tabs-item title="app.component.ts" %}
```typescript
import { Component } from '@angular/core';

// 팝콘 서비스를 불러옵니다.
import { PopcornService } from './popcorn.service';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css'],

  // 컴포넌트에 팝콘 서비스를 공급합니다.
  provides: [PopcornService]
})
export class AppComponent {

  // 생성자에 팝콘 서비스를 주입합니다.
  constructor(private popcornService:PopcornService) {}
  
  cookIt(quantity:number):void {
    // 팝콘 서비스 객체의 cook() 메서드를 실행합니다.
    this.popcornService.cook(quantity);
  }
  
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

컴포넌트 템플릿에서 `cookIt()` 메서드를 호출하면 컴포넌트 내부에서 팝콘 서비스를 사용합니다.

```markup
<label for="popcorn">팝콘</label>
<input id="popcorn" type="number" #quantity placeholder="조리할 팝콘 통 수 입력">
<button type="button" (click)="cookIt(quantity.value)">조리</button>
```

### 라이프 사이클 훅

생성자는 복잡한 로직, 특히 데이터 접근 메소드와 같이 서버를 호출하는 로직을 포함해서는 안됩니다. 생성자는 프로퍼티를 생성자 파라미터와 연결하는 것과 같은 간단한 초기화를 위한 것입니다.

서비스 객체에서 특정 데이터를 가져올 경우, `ngOnInit` [라이프 사이클 훅](../comp-communication/life-cycle.md#ngoninit)을 사용할 수 있습니다. Angular는 컴포넌트 라이프 사이클의 각 순간\(생성, 변경, 파괴 등\)의 작업을 위한 인터페이스를 제공합니다.

{% code-tabs %}
{% code-tabs-item title="app.component.ts" %}
```typescript
import { Component, OnInit } from '@angular/core';
import { PopcornService } from './popcorn.service';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css'],
  provides: [PopcornService]
})
export class AppComponent implements OnInit {
  
  // 생성자는 의존성 모듈 주입 및 속성 설정에 사용됩니다.
  constructor(private popcornService:PopcornService) {}
  
  ngOnInit():void {
    // 서비스 객체로부터 특정 데이터를 가져오는 등 특정 로직이 필요한 경우,
    // 라이프 사이클 훅을 사용합니다.
  }
  
  cookIt(quantity:number):void {
    // 팝콘 서비스 객체의 cook() 메서드를 실행합니다.
    this.popcornService.cook(quantity);
  }
  
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### 프로미스

ES6의 [Promise](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Promise)는 결과가 준비될 때 콜백 할 것을 약속합니다. 서비스의 처리가 비동기 적으로 수행될 때, 콜백 기능을 제공하도록 요청할 수 있습니다. 아래 예제 코드에서는 비동기를 시뮬레이션 하는 코드를 통해 프로미스가 처리하는 결과를 확인할 수 있습니다.

{% code-tabs %}
{% code-tabs-item title="data.service.ts" %}
```typescript
import { Injectable } from '@angular/core';

const DATA: string[] = [
  'promise',
  'async await',
  'arrow function'
];

@Injectable()
export class DataService {
  
  constructor() {}
  
  getData():Promise<string[]> {
    // Promise.resolve() 스태틱 메서드를 활용해 DATA를 반환합니다.
    return Promise.resolve(DATA);
  }
  
  getAsyncData(ms:number = 2000):Promse<string[]> {
    // 특정 시간을 두고, getData() 메서드를 실행해 Promse 객체를 반환합니다.
    return new Promise(resolve => window.setTimeout(() => this.getData(), ms));
  }
  
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

컴포넌트 라이프 사이클 훅 메서드 내부에서 서비스를 통해 데이터를 가져와 컴포넌트 속성에 할당할 수 있습니다.

{% code-tabs %}
{% code-tabs-item title="app.component.ts" %}
```typescript
import { Component, OnInit } from '@angular/core';
import { DataService } from './data.service';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css'],
  provides: [DataService]
})
export class AppComponent implements OnInit {
  
  data:string[];
  
  constructor(private dataService:DataService) {}
  
  ngOnInit():void {
    this.dataService.getAsyncData(3000).then(data => this.data = data);
  }
  
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

