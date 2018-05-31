# 콘텐츠 전달/삽입

자식 컴포넌트 템플릿 마크업 코드 중, 일부를 부모 컴포넌트에서 전달하여 처리하게 만들 수 있습니다. 자식 컴포넌트 내부 구성이 매번 변경될 필요가 있다면 자식 컴포넌트가 아닌, 부모 컴포넌트 템플릿에서 유연하게 변경 가능해집니다.

{% code-tabs %}
{% code-tabs-item title="자식 컴포넌트 템플릿" %}
```markup
<li class="list-group-item">
  <h4>{{ item.title }}</h4>
  <p>{{ item.description }}</p>
</li>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="부모 컴포넌트 템플릿" %}
```markup
<app-list-item *ngFor="let item of lists" [item]="item"></app-list-item>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

먼저 외부에서 전달 받을 자식 컴포넌트 마크업 코드 중 일부를 제거하고, 그 자리에 \`&lt;ng-content&gt;\`를 추가합니다. 눈치 채셨죠? \`&lt;ng-content&gt;\`는 외부에서 전달 받은 콘텐츠가 끼워지는 슬롯\(Slot\)과 같습니다.

{% code-tabs %}
{% code-tabs-item title="자식 컴포넌트 템플릿" %}
```markup
<li class="list-group-item">
  <ng-content></ng-content>
</li>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

부모 컴포넌트 템플릿에서 자식 컴포넌트 커스텀 요소 내부에 마크업을 추가 작성하면 해당 코드는 \`&lt;ng-content&gt;\` 위치로 삽입 됩니다. 

{% code-tabs %}
{% code-tabs-item title="부모 컴포넌트 템플릿" %}
```markup
<app-list-item *ngFor="let item of lists" [item]="item">
  <!-- 슬롯 콘텐츠 -->  
  <h4>{{ item.title }}</h4>
  <p>{{ item.description }}</p>
  <!--// 슬롯 콘텐츠 -->  
</app-list-item>
```
{% endcode-tabs-item %}
{% endcode-tabs %}



