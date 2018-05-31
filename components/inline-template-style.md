# 인라인 템플릿 / 스타일링

간단한 컴포넌트의 경우, 별도의 HTML, CSS 파일을 만드는 것에 회의적일 수 있습니다. 이런 경우, 컴포넌트 파일\(`<컴포넌트-이름>.component.ts`\) 내부에 인라인 템플릿, 스타일링 코드를 삽입하여 처리할 수 있습니다.

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

