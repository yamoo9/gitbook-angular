# 속성 바인딩

데이터 값을 가진 속성 이름을 템플릿 마크업의 속성에 할당하면 데이터 바인딩이 처리됩니다. Angular는 일반 속성과 달리 각괄호\(`[]`\)로 묶인 속성을 찾아 데이터 바인딩 합니다.

{% code-tabs %}
{% code-tabs-item title="app/button/button.component.ts" %}
```typescript
@Component(metadata)
export class ButtonComponent {

  public content:     string  = '메뉴 토글';
  public type:        string  = 'button';
  public is_disabled: boolean = false;

}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

버튼 컴포넌트 클래스에 설정된 데이터 이름을 템플릿 마크업에 설정하는 HTML 코드를 살펴보세요.

**HTML**

{% code-tabs %}
{% code-tabs-item title="app/button/button.component.html" %}
```markup
<button
  class="btn btn-primary"
  [type]="type"
  [disabled]="is_disabled">
  {{ content }}
</button>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## 문자 인터폴레이션 방식을 대체하는 속성 바인딩 방법

문자 인터폴레이션 방식 말고도 `[innerText]` 바인딩 속성을 사용해 `content` 속성 값을 바인딩 할 수 있습니다. 물론, 문자 인터폴레이션 코드는 제거해야겠죠!

**HTML**

{% code-tabs %}
{% code-tabs-item title="app/button/button.component.html" %}
```markup
<button
  class="btn btn-primary"
  [type]="type"
  [innerText]="content"></button>
```
{% endcode-tabs-item %}
{% endcode-tabs %}



