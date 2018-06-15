# 파이프

파이프\(Pipe\)는 AngularJS\(v1\)에서 필터\(Filter\)라고 불렸고, 사용법은 동일합니다. 파이프는 HTML 템플릿에서 값의 표시 형태를 변환해 보여주기 위한 용도로 사용합니다. 모든 글자를 대문자\(uppercase\) 또는 소문자\(lowercase\)로 변경 한다거나,  숫자\(number\) 값을 3자리 마다 콤마\(,\)로 구분 한다거나, 화폐\(currency\) 값을 변경 할 수 있습니다.

![Angular Pipe\(\|\)](.gitbook/assets/image%20%289%29.png)

## 파이프 문법

템플릿 스트링 인터폴레이션 구문 입력 값 뒤에 파이프\(`|`\)를 붙이면, Angular는 입력 값을 정의된 파이프를 사용해 값을 변경한 후, 반환합니다.

{% code-tabs %}
{% code-tabs-item title="파이프 기본 사용법" %}
```markup
{{ input | pipe }}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

파이프는 함수를 호출해 실행한 후, 결과 값을 반환 하므로 매개변수를 전달 받아 다양하게 응용할 수 있습니다.

{% code-tabs %}
{% code-tabs-item title="파이프에 매개변수를 전달" %}
```markup
<!-- 매개변수 1개 전달 -->
{{ input | pipe: param }}

<!-- 매개변수 2개 이상 전달 -->
{{ input | pipe: param1 : param2 : ... : paramN }}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

파이프는 결과 값을 돌려 주므로 파이프를 연이어 사용할 수 있습니다. 모든 파이프를 거친 값을 최종 출력합니다.

{% code-tabs %}
{% code-tabs-item title="파이프 체인 사용법" %}
```markup
{{ input | pipe1 | pipe2 | ... | pipeN }}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## 빌트인 파이프

Angular는 유용한 파이프를 사용자에게 제공합니다. [기본 제공되는 빌트인 파이프](https://angular.io/api?type=pipe) 목록은 다음과 같습니다. 참고로 `Deprecated*Pipe`는 사용을 금하는 이전의 파이프 입니다.

![Angular &#xBE4C;&#xD2B8;&#xC778; &#xD30C;&#xC774;&#xD504; &#xB9AC;&#xC2A4;&#xD2B8;](.gitbook/assets/image%20%282%29.png)

### uppercase 파이프

영문을 모두 대문자로 변경\([UpperCasePipe](https://angular.io/api/common/UpperCasePipe)\) 합니다.

{% code-tabs %}
{% code-tabs-item title="템플릿\(Template\)" %}
```markup
<p>{{ 'this is pipe.' | uppercase }}</p>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="뷰\(View\) : 결과" %}
```markup
<p>THIS IS PIPE.</p>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### lowercase 파이프

영문을 모두 소문자로 변경\([LowerCasePipe](https://angular.io/api/common/LowerCasePipe)\) 합니다.

{% code-tabs %}
{% code-tabs-item title="템플릿\(Template\)" %}
```markup
<p>{{ 'I Want Change english text to LowerCASE.' | lowercase }}</p>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="뷰\(View\) : 결과" %}
```markup
<p>i want change english text to lowercase.</p>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### titlecase 파이프

공백으로 구분되는 영 단어의 첫글자를 모두 대문자 화하는 타이틀 케이스로 변경\([TitleCasePipe](https://angular.io/api/common/TitleCasePipe)\) 합니다.

{% code-tabs %}
{% code-tabs-item title="템플릿\(Template\)" %}
```markup
<p>{{ 'I want change english-text to title|case.' | titlecase }}</p>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="뷰\(View\) : 결과" %}
```markup
<p>I Want Change English-text To Title|case.</p>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### percent 파이프

소수점 숫자 값을 퍼센트\(%\)로 변경\([PercentPipe](https://angular.io/api/common/PercentPipe)\)합니다. 퍼센트 파이프는 매개변수를 전달해 값을 다양하게 변경할 수 있습니다. 매개변수 '`n.x-y`'에서 `n`은 소수점 앞자리 글자 설정이며, `x`는 최소 소수점 글자 개수, `y`는 최대 소수점 글자 개수입니다.

{% code-tabs %}
{% code-tabs-item title="템플릿\(Template\)" %}
```markup
<!-- 기본 사용법 -->
<p>{{ 0.341 | percent }}</p>

<!-- 매개변수 전달 -->
<p>{{ 0.345124 | percent: '2.2-3' }}</p>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="뷰\(View\) : 결과" %}
```markup
<p>34%</p>
<p>34.512%</p>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### decimal 파이프

숫자 또는 소수점 숫자 값을 변경\([DecimalPipe](https://angular.io/api/common/DecimalPipe)\) 합니다. 정수 부분은 3자리 마다 콤마\(,\)를 붙이고 소수 부분은 별도의 설정이 없을 경우 반올림 후 3자리에서 끊습니다. 매개변수 설정은 퍼센트 파이프와 동일합니다.

{% code-tabs %}
{% code-tabs-item title="템플릿\(Template\)" %}
```markup
<!-- 기본 사용법(소수점 3자리까지 출력) -->
<p>{{ 1981.0191 | number }}</p>

<!-- 매개변수 전달(정수 부분 5글자, 소수 부분 최소 4 - 최대 6 글자) -->
<p>{{ 2018.0612345891 | number: '5.4-6' }}</p>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="뷰\(View\) : 결과" %}
```markup
<p>1,981.019</p>
<p>02,018.061235</p>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### currency 파이프

숫자 값을 화폐 값으로 변경\([CurrencyPipe](https://angular.io/api/common/CurrencyPipe)\) 합니다. 기본 값은 미국 화폐 단위\($\)가 사용됩니다. 대한민국 화폐\(₩\) 단위를 사용하려면 매개변수 값으로 화폐 코드를 설정해야 합니다. 숫자 파이프처럼 소수점 설정도 가능하지만, 대한민국 화폐 단위에서는 소수점을 사용하지 않아 유용하지 않습니다.

{% code-tabs %}
{% code-tabs-item title="템플릿\(Template\)" %}
```markup
<!-- 기본 사용법(소수점 2자리까지 출력) -->
<p>{{ 10000 | currency }}</p>

<!-- 매개변수 전달(국제 화폐 코드: USD, CAD, KRW) -->
<p>{{ 10000 | currency: 'KRW' }}</p>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="뷰\(View\) : 결과" %}
```markup
<p>$10,000.00</p>
<p>₩10,000</p>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% hint style="info" %}
각 나라별 화폐 코드는 [ISO 4217](https://ko.wikipedia.org/wiki/ISO_4217)에서 확인하세요.
{% endhint %}

### date 파이프

Date 객체의 정보 값을 날짜 값으로 변경\([DatePipe](https://angular.io/api/common/DatePipe)\) 합니다. 기본 값은 영문권 날짜 정보라, 대한민국 날짜 정보로 변경 하려면 매개변수를 사용해 설정해야 합니다. 보다 자세한 사용법은 [날짜 포멧 설명](https://angular.io/api/common/DatePipe#description)을 살펴보세요.

{% code-tabs %}
{% code-tabs-item title="템플릿\(Template\)" %}
```markup
<!-- 기본 사용법(※ Date.now() 값을 숫자로 변경) -->
<p>{{ 1529038096593 | date }}</p>

<!-- 매개변수 전달(년, 월, 일) -->
<p>{{ 1529038096593 | date: 'yyyy년 M월 d일' }}</p>

<!-- 매개변수 전달(12시, 분, 초) -->
<p>{{ 1529038096593 | date: 'h시 m분 s초' }}</p>

<!-- 매개변수 전달(24시, 분, 초) -->
<p>{{ 1529038096593 | date: 'H시 m분 s초' }}</p>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="뷰\(View\) : 결과" %}
```markup
<p>Jun 15, 2018</p>
<p>2018년 6월 15일</p>
<p>1시 48분 16초</p>
<p>13시 48분 16초</p>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### JSON 파이프

JSON 문자 값을 JavaScript 객체 값으로 변경\([JsonPipe](https://angular.io/api/common/JsonPipe)\) 합니다. 객체 값을 디버깅 용도로 사용할 수 있습니다.

{% code-tabs %}
{% code-tabs-item title="템플릿\(Template\)" %}
```markup
<!-- routerLink는 컴포넌트에 설정된 속성(객체 타입) -->
<pre>{{ routerLink | json }}</pre>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="뷰\(View\) : 결과" %}
```markup
<pre>
[
  {
    "label": "홈",
    "link": ""
  },
  {
    "label": "카테고리",
    "link": "categories"
  },
  {
    "label": "태그",
    "link": "tags"
  }
]
</pre>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### slice 파이프

문자 값에서 설정된 매개변수에 따라 잘라낸 값으로 변경\([SlicePipe](https://angular.io/api/common/SlicePipe)\) 합니다. 사용법은 JavaScript 배열\(Array\) 객체의 slice\(\) 메서드와 유사합니다. 

{% code-tabs %}
{% code-tabs-item title="템플릿\(Template\)" %}
```markup
<!-- start:0 / end:4 -->
<p>{{ '대한민국 태극전사 파이팅!' | slice:0:4 }}</p>

<!-- start:5 / end:9 -->
<p>{{ '대한민국 태극전사 파이팅!' | slice:5:9 }}</p>

<!-- start:-4 -->
<p>{{ '대한민국 태극전사 파이팅!' | slice:-4 }}</p>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="뷰\(View\) : 결과" %}
```markup
<p>대한민국</p>
<p>태극전사</p>
<p>파이팅!</p>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

#### 리스트 + 슬라이스 파이프

`*ngFor` 디렉티브 구문 뒤에 파이프를 붙여 사용할 수도 있습니다.

{% code-tabs %}
{% code-tabs-item title="sliceListPipeDemo.Component.ts" %}
```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'slice-list-pipe',
  template: `
  <ol>
    <li *ngFor="let item of lists | slice:1:3">{{ item }}</li>
  </ol>
  `
})
export class SliceListPipeDemoComponent {
  lists:string[] = '러시아 2018 월드컵 대한민국 태극전사 파이팅'.split(' ');
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="뷰\(View\) : 결과" %}
```markup
<ul>
  <li>2018</li>
  <li>월드컵</li> 
</ul>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### I18nSelect 파이프

객체의 속성과 일치할 경우, 값을 반환\([I18nSelectPipe](https://angular.io/api/common/I18nSelectPipe)\) 합니다. 예를 들어 각 나라별 인사말을 값으로 하는 객체에서 나라 식별자와 일치하는 값을 반환합니다. 일치하는 값이 없을 경우, 빈 문자열을 반환합니다.

{% code-tabs %}
{% code-tabs-item title="I18nSelectDemo.component.ts" %}
```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'i18n-select-demo',
  template: `
    <p>greeting | i18nSelect: greeting_map</p>
  `
})
export class I18nSelectDemoComponent {
  greeting:string = 'ko';
  greeting_map:objet = { 
    'ko': '안녕하세요',
    'en': 'Hello', 
    'zh': '你好', 
    'ja': 'こんにちは', 
    'es': 'Buenos dias',
  };
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="뷰\(View\) : 결과" %}
```markup
<p>안녕하세요</p>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### I18nPlural 파이프

데이터 갯수를 파악하여 결과 값을 도출\([I18nPluralPipe](https://angular.io/api/common/I18nPluralPipe)\) 합니다. 예를 들어 댓글 정보를 담은 배열이 있을 때, 댓글 배열 아이템 갯수를 파악하여 갯수와 일치하는 메시지를 화면에 출력합니다.

{% code-tabs %}
{% code-tabs-item title="I18nSelectDemo.component.ts" %}
```typescript
import { Component } from '@angular/core';

@Component({ 
  selector: 'i18n-plural-pipe', 
  template: `
    <span class="comments-info">
      {{ comments.length | i18nPlural: comments_map }}
    </span>
  `
})
export class I18nPluralComponent {
  comments:any[] = ['댓글 1', '댓글 2'];
  comments_map:{[C:string]: string} = {
    '=0': '댓글이 없어요.',
    'other': '댓글 #'
  };
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="뷰\(View\) : 결과" %}
```markup
<span class="comments-info">댓글 2</span>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### async 파이프

Promise 객체의 이행\(resolve\) 결과를 비동기 데이터로 받아 출력\([asyncPipe](https://angular.io/api/common/AsyncPipe)\) 합니다.

{% code-tabs %}
{% code-tabs-item title="asyncPipe.component.html" %}
```markup
<div class="async-demo"> 
  
  <button 
    type="button" 
    class="btn btn-outline-primary mt-3" 
    (click)="onResolve()"> 
    {{received ? '초기화(reset)' : '이행(resolve)'}} 
  </button>
  
  <div class="card text-white bg-primary mt-3" style="max-width: 480px;"> 
    <div class="card-header">Promise 데이터 비동기 처리</div> 
    <div class="card-body"> 
      <p class="card-text">데이터 수신 대기 중: {{ received_data | async }}</p> 
    </div> 
  </div> 
  
</div>
```
{% endcode-tabs-item %}

{% code-tabs-item title="asyncPipe.component.ts" %}
```typescript
import { Component } from '@angular/core';

@Component({ 
  selector: 'async-pipe-demo',
  templateUrl: './asyncPipe.component.html',
})
export class AsyncPipeComponent {

  received:boolean = false;
  resceive_data:Promise<string>|null = null;
  
  private _resolve:Function|null = null;
  
  constructor() {
    this.reset();
  }
  
  reset():void {
    this.received = false;
    this.resceive_data = new Promise<string>(resolve => {
      this._resolve = resolve;
    });
  }
  
  onResolve():void {
    if (this.received) {
      this.reset();
    } else {
      window.setTimeout(()=>{
        this._resolve('Promise 이행 데이터');
        this.received = true;
      }, 1000);
    }
  }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

`async` 파이프는 [Observable](https://angular.io/guide/observables) 에서도 활용할 수 있습니다.

```typescript
import { Component } from '@angular/core';
import { Observable, Observer } from 'rxjs';

@Component({ 
  selector: 'async-observable-pipe', 
  template: `
    <time [datetime]="date_time">{{ time | async }}</time>
  ` 
}) 
export class AsyncObservablePipeComponent {
  
  date_time:string = '';
  
  time = new Observable<string>((o:Observer<string>)=>{
    window.setInterval(()=> {
      const d = new Date();
      this.date_time = d.toTimeString();
      o.next( d.toLocaleTimeString() );
    });
  });
  
}
```

