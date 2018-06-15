# 커스텀 파이프

사용자가 직접 파이프를 제작해 프로젝트에 활용할 수도 있습니다. 커스텀 파이프를 제작하려면 Pipe, PipeTransform을 불러와 사용합니다. `@Pipe` 데코레이터에 파이프 식별자로 사용할 `name` 속성 값을 입력한 후, `transform()` 함수 내부에 파이프 로직을 작성합니다. 

작성이 마무리 된 파이프는 모든 컴포넌트에서 사용할 수 있도록 app.module.ts 파일에 등록해야 합니다.

### 숫자 앞에 0을 붙이는 파이프

숫자 값이 10보다 작을 경우, 숫자 앞에 0을 붙이는 파이프입니다.

{% code-tabs %}
{% code-tabs-item title="app.module.ts" %}
```typescript
import { ReadingZeroPipe } from './pipe/readingZero.pipe';

@NgModule({
  declarations: [
    // ...
    ReadingZeroPipe
  ]
});
```
{% endcode-tabs-item %}

{% code-tabs-item title="readingZero.ts" %}
```typescript
import { Pipe, PipeTransform } from '@angular/core';

@Pipe({
  name: 'readingZero'
})
export class ReadingZeroPipe implements PipeTransform {
  transform(value:number):string {
    return value > 10 ? String(value) : `0${value}`;
  }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

```markup
<p>{{ 9 | readingZero }}</p> <!-- 09 -->
```

### 텍스트 생략 파이프

텍스트 길이를 제한한 경우, 제한된 길이보다 긴 텍스트는 제거하여 생략\(Ellipsis\) 처리하는 파이프입니다.

{% code-tabs %}
{% code-tabs-item title="app.module.ts" %}
```typescript
import { EllipsisPipe } from './pipe/ellipsis.pipe';

@NgModule({
  declarations: [
    // ...
    EllipsisPipe
  ]
});
```
{% endcode-tabs-item %}

{% code-tabs-item title="ellipsis.pipe.ts" %}
```typescript
import { Pipe, PipeTransform } from '@angular/core';

@Pipe({
  name: 'ellipsis'
})
export class EllipsisPipe implements PipeTransform {
  transform(value:string, limit:number = 300):string {
    if ( value.length > limit ) {
      return `${value.slice(0, limit+1)}...`;
    } else {
      return value;
    }
  }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

```markup
<p>{{ '텍스트 생략은 .....' | ellipsis: 80 }}</p>
```

### 대한민국 화폐\(원\) 파이프

Angular 파이프 currency는 대한민국 화폐\(원\)를 처리할 수 없습니다. 이를 처리하는 원\(Won\) 파이프입니다. 작성된 코드를 살펴보면 파이프 내에서 빌트인 파이프를 불러와 사용할 수도 있습니다.

{% code-tabs %}
{% code-tabs-item title="app.module.ts" %}
```typescript
import { WonPipe } from './pipe/won.pipe';

@NgModule({
  declarations: [
    // ...
    WonPipe
  ]
});
```
{% endcode-tabs-item %}

{% code-tabs-item title="won.pipe.ts" %}
```typescript
import { Pipe, PipeTransform } from '@angular/core';
import { DecimalPipe } from '@angular/common';

@Pipe({
  name: 'won'
})
export class WonPipe implements PipeTransform {
  transform(value:number):string {
    let d = new DecimalPipe('en-US');
    return `${d.transform(value, '1.0-0')}원`;
  }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

```markup
<p>{{10000 | won}}</p> <!-- 10,000원 -->
```

