# 이벤트 바인딩

템플릿 마크업에 `(이벤트-타입)` 속성 값으로 메서드를 연결하면 Angular는 이벤트 바인딩을 처리합니다.

{% code-tabs %}
{% code-tabs-item title="app/button/button.component.ts" %}
```typescript
@Component(metadata)
export class ButtonComponent {

  public content:     string  = '토글 ON';
  public type:        string  = 'button';
  public is_disabled: boolean = false;

  // 토글 상태 변경 메서드
  public onChangeStateToggle(): void {
    this.content = this.content.includes('ON') ? '토글 OFF' : '토글 ON';
  }

}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

버튼 요소의 `(click)` 속성에 `onChangeStateToggle()` 메서드를 바인딩 했습니다. 버튼을 클릭하면 버튼 콘텐츠 값이 `ON` 또는 `OFF`로 토글 됩니다.

{% code-tabs %}
{% code-tabs-item title="app/button/button.component.html" %}
```markup
<button
  class="btn btn-primary"
  [type]="type"
  [disabled]="is_disabled"
  (click)="onChangeStateToggle()">
  {{ content }}
</button>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## 이벤트 객체 전달인자

Angular는 이벤트 속성\(`(input)`\)에 연결된 메서드를 통해 이벤트 객체\(`$event`\)를 전달 받을 수 있습니다. 이를 통해 사용자가 입력한 정보 데이터를 컴포넌트로 전달할 수 있습니다.

{% code-tabs %}
{% code-tabs-item title="app/input/input.component.ts" %}
```typescript
@Component(metadata)
export class InputComponent {

  public label_id:            string = 'y9-username';
  public label_conetnt:       string = '사용자 이름';
  public type:                string = 'text';
  private pass_by_user_input: string = '';

  onPasssingByUserInput($event): void {
    this.pass_by_user_input = $event.target.value;
  }

}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

`(input)` 이벤트 속성에 연결된 `onPasssingByUserInput()` 메서드에 `$event` 객체를 전달하면 메서드는 인자 값을 통해 사용자가 입력한 값\(`$event.target.value`\) 값을 받아 올 수 있습니다. 받아 온 값을 `pass_by_user_input` 값에 할당하면 사용자의 UI도 즉시 업데이트 되는 것을 확인할 수 있습니다.

{% code-tabs %}
{% code-tabs-item title="app/input/input.component.html" %}
```markup
<div class="input-group mb-3">
  <div class="input-group-prepend">
    <label
      class="input-group-text"
      [for]="label_id"
      [attr.aria-label]="label_content">@</label>
  </div>
  <input
    class="form-control"
    [id]="label_id"
    [type]="type"
    [placeholder]="label_content"
    (input)="onPasssingByUserInput($event)">
</div>

<!-- 사용자 입력 내용 출력 -->
<p class="lead">
  사용자 입력 내용: <b>{{ pass_by_user_input }}</b>
</p>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% hint style="info" %}
**NOTE.**  
안타깝게도 Angular는 현재\(2018.06\) WAI-ARIA 속성을 동적으로 데이터 바인딩하는 것을   
지원하지 않습니다. 이런 경우 동적으로 속성 값을 할당 하려면 `[attr.aria-label]` 방법을   
사용해야 합니다.
{% endhint %}



