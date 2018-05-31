# 뷰 인캡슐레이션

\[ViewEncapsulation\]\[1\]은 컴포넌트 스타일을 컴포넌트 독립적으로 사용할지 유무를 결정할 때 사용합니다. 즉, 컴포넌트 스타일시트 파일에 작성한 코드를 컴포넌트에 한해 동작하도록 할지 설정하는 것이죠. 이를 스타일 캡슐화라고 부릅니다.

`ViewEncapsulation`은 `enum` 타입 입니다. `enum` 타입은 TypeScript에서 지원하는 데이터 유형으로 숫자를 기억하기 용이하도록 할 때 사용됩니다. \(JavaScript에서는 지원하지 않습니다\)

```typescript
enum ViewEncapsulation {
  Emulated: 0,
  Native: 1,
  None: 2
}
```

| 속성 | 값 | 설명 |
| --- | --- | --- |
| Emulated | 0 | Angular 식별 ID를 통해 스타일 캡슐화 \(기본 값\) |
| Native | 1 | 렌더러의 기본 캡슐화 메커니즘을 사용 \([Shadow DOM](https://w3c.github.io/webcomponents/spec/shadow/) 사용\) |
| None | 2 | 스타일 캡슐화를 하지 않음 |

컴포넌트 스타일 캡슐화를 사용하지 않으려면 `@Component()` 컴포넌트 데코레이터에 `encapsulation` 속성 값으로 `ViewEncapsulation.None`을 설정합니다.

```typescript
import { Component } from "@angular/core";

@Component({
  selector: 'app-view-encapsulation',
  template: `<p>스타일 캡슐화</p>`,
  styles: `p { color: #00d8d6; }`, // 이 스타일은 캡슐화 되지 않습니다.
  encapsulation: ViewEncapsulation.None // Emulated, Native, None
})
export class ViewEncapsulationComponent {

}
```

\[1\]: [https://angular.io/api/core/ViewEncapsulation](https://angular.io/api/core/ViewEncapsulation)

