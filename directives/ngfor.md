# \*ngFor 디렉티브

`*ngFor` 디렉티브는 `&ngIf` 디렉티브와 마찬가지로 구조 디렉티브입니다. 데이터를 따라 반복된 구성을 완성한 후, 화면에 렌더링 합니다. AppComponent 에서 ButtonComponent를 자식 컴포넌트로 사용하는 예제를 통해 `*ngFor` 디렉티브를 공부해봅니다.

AppComponent 뷰에서 '보임', '감춤', '토글'을 콘텐츠로 하는 3개의 버튼을 생성해야 할 경우, `<app-button>` 요소를 3번 복사/붙여넣기 해서 구성할 수 있습니다. 하지만 이 방법은 반복해서 생성될 컴포넌트의 갯수가 많아질수록 효율이 떨어지게 됩니다. 이러한 경우 for 문을 사용해 효율성을 높인 것과 동일하게 `*ngFor` 디렉티브를 사용해 효율성과 생산성을 높일 수 있습니다.

먼저 반복할 데이터를 정의해야 합니다. AppComponent에 `buttons` 속성에 3개의 아이템을 가진 배열을 설정합니다.

{% code-tabs %}
{% code-tabs-item title="app/app.component.ts" %}
```typescript
import { Component } from '@angular/core';

@Component(metadata)
export class AppComponent {

  public title:string     = 'Angular *ngFor 디렉티브';
  public buttons:string[] = ['보임', '감춤', '토글'];

}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

이어서 AppComponent 템플릿 파일 `<app-button>` 요소를 작성한 후, `*ngFor` 디렉티브를 통해 AppComponent의 `buttons` 배열 데이터를 반복하여 구조를 동적으로 생성할 수 있습니다. 구문은 ES6에 추가된 `for - of` 문과 유사합니다.

{% code-tabs %}
{% code-tabs-item title="app/app.component.html" %}
```markup
<app-button *ngFor="let button of buttons"></app-button>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## \*ngFor 로컬 변수

`*ngFor` 디렉티브는 템플릿에서 사용 가능한 로컬 변수를 제공합니다.

* `index` : 개별 항목 인덱스
* `odd` : 홀수 항목
* `even` : 짝수 항목
* `first` : 첫번째 항목
* `last` : 마지막 항목

이를 활용하여 조건에 따라 다른 결과를 프로그래밍 할 수 있습니다.

```markup
<app-button
  *ngFor="let button of buttons; let i = index; first as is_first"
  [title]="`${i}번째 요소는 첫번째 버튼 요소가 ${is_first ? '맞습니다.': '아닙니다.'}`">
</app-button>
```



