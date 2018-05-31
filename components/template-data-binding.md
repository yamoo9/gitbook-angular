# 템플릿 / 데이터 바인딩

## 템플릿\(Template\)

컴포넌트 메타데이터에 설정된 `templateUrl` 속성 값을 통해 Angular는 컴포넌트 템플릿을 찾습니다. 버튼 컴포넌트 템플릿으로 사용할 HTML 파일 `button.component.html` 파일을 `app/button/` 디렉토리 내부에 생성합니다.

템플릿으로 사용할 HTML 구조를 마크업 합니다.

{% code-tabs %}
{% code-tabs-item title="app/button/button.component.html" %}
```markup
<button type="button">버튼 컴포넌트</button>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## 컴포넌트 등록

생성한 버튼 컴포넌트를 애플리케이션에서 사용하려면 `app/app.module.ts` 파일에 불러와 `@NgModule` 선언\(`declarations`\)에 추가해야 합니다.

{% code-tabs %}
{% code-tabs-item title="app/app.module.ts" %}
```typescript
import { ButtonComponent } from "./button/button.component";

@NgModule({
  declarations: [
    AppComponent,
    ButtonComponent
  ],
  ...
})
export class AppModule { }
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## 컴포넌트 사용

{% code-tabs %}
{% code-tabs-item title="app/app.component.html" %}
```markup
<app-button></app-button>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## 컴포넌트 스타일 설정

컴포넌트를 스타일링하고자 한다면 `app/button` 디렉토리에 `button.component.css` 파일을 생성한 후, 버튼 컴포넌트 스타일 코드를 작성합니다.

{% code-tabs %}
{% code-tabs-item title="app/button/button.component.css" %}
```css
button {
  cursor: pointer;
  border: none;
  border-radius: 4px;
  padding: 0.8em 1em;
  background: #efefef;
  color: #212121;
}

button.is-small {
  font-size: 12px;
}

button.is-big {
  font-size: 18px;
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% hint style="info" %}
**NOTE**.  
`button` 선택자를 사용했지만, 컴포넌트 내부에 연결된 CSS 코드는 컴포넌트 독립적으로 적용됩니다. 자세한 내용은 [뷰 인캡슐레이션](https://uid.gitbook.io/angular/~/edit/primary/components/template-data-binding)에서 확인해보세요. 

컴포넌트 독립적으로 적용된 선택자: `button[_ngcontent-c1]`
{% endhint %}





