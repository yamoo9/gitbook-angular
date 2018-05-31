# 인라인 템플릿 / 스타일링

간단한 컴포넌트의 경우, 별도의 HTML, CSS 파일을 만드는 것에 회의적일 수 있습니다. 이런 경우, 컴포넌트 파일\(`<컴포넌트-이름>.component.ts`\) 내부에 인라인 템플릿, 스타일링 코드를 삽입하여 처리할 수 있습니다.

{% code-tabs %}
{% code-tabs-item title="app/checkbox/checkbox.component.ts" %}
```typescript
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-checkbox',
  template: `
    <label class="checkbox">
      <input type="checkbox"> 체크박스 컴포넌트
    </label>
  `,
  styles: [
    `.checkbox {
        color: #900;
      }
      input[type="checkbox"] {
        vertical-align: middle;
      }`
  ]
})
// OnInit 인터페이스에 따르는 CheckboxComponent 컴포넌트 클래스
export class CheckboxComponent implements OnInit {

  constructor() { }

  ngOnInit() { } // 필수! 해당 메서드를 제외하면 오류 발생

}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% hint style="info" %}
**NOTE.**  
프로젝트 팀원 중 컴포넌트가 아닌, HTML, CSS를 별도로 수정해야 할 경우는   
별도의 템플릿, 스타일 파일을 유지하는 것이 보다 권장됩니다.
{% endhint %}



