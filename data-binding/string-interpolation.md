# 문자 인터폴레이션

TypeScript 클래스에 설정된 속성 데이터 값을 연결된 템플릿 내부에 `{{ }}` 기호를 사용해 바인딩 할 수 있습니다. `ButtonComponent` 클래스에 `content` 속성\(타입 지정\)을 추가하면 데이터가 설정됩니다.   
템플릿에 `{{ content }}` 마크업을 추가하면 데이터가 바인딩 됩니다.

{% code-tabs %}
{% code-tabs-item title="app/button/button.component.ts" %}
```typescript
@Component(metadata)
export class ButtonComponent {

  public content:string;

  constructor() {
    this.content = '메뉴 토글';
  }

}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="app/button/button.component.html" %}
```markup
<button type="button" class="btn btn-primary">{{ content }}</button>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## 비공개 속성과 메서드 활용

TypeScript 접근 제어자 `private`를 사용하면 속성을 외부에서 접근할 수 없도록 감출 수 있습니다. 오직 비공개 속성에 접근 가능한 메서드를 클래스 내에 정의한 후, 활용하는 방법을 사용할 수도 있습니다.

{% code-tabs %}
{% code-tabs-item title="app/button/button.component.ts" %}
```typescript
@Component(metadata)
export class ButtonComponent {

  private _content:string;

  constructor() {
    this._content = '메뉴 토글';
  }

  getContent(): string {
    return this._content;
  }

}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="app/button/button.component.html" %}
```markup
<button type="button" class="btn btn-primary">{{ getContent() }}</button>
```
{% endcode-tabs-item %}
{% endcode-tabs %}



