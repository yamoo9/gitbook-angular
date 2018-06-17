# Angular Material

[Angular Material](https://material.angular.io/)은 Angular를 위한 Material 디자인 컴포넌트 모음으로 웹, 모바일, 데스크톱 환경에서 작동하는 모던한 UI 컴포넌트를 사용할 수 있습니다. Angular와 완벽한 통합을 위해 Angular 팀에서 제작한 프레임 워크입니다.

## 개발 모듈 설치

[Guides](https://material.angular.io/guide/getting-started)에 따라 설치를 진행해보겠습니다. Angular Material을 프로젝트에 사용하기 위해서는 `material`, `cdk` 2개의 개발 모듈을 설치해야 합니다.

```bash
$ npm i @angular/material @angular/cdk
```

## 애니메이션 모듈 설치

이어서 애니메이션\(`animations`\) 모듈을 설치 합니다. Angular Material 컴포넌트 중 애니메이션에 의존하기 때문에 애니메이션 모듈 설치가 필요합니다.

```bash
$ npm i @angular/animations
```

루트 모듈인 `app.modules.ts` 파일에 `BrowserAnimationsModule` 모듈을 임포트 한 후, `@NgModule()`의 `imports` 항목에 추가합니다.

{% code-tabs %}
{% code-tabs-item title="src/app.modules.ts" %}
```typescript
import {BrowserAnimationsModule} from '@angular/platform-browser/animations';

@NgModule({
  ...
  imports: [
    BrowserModule,
    BrowserAnimationsModule,
  ],
  ...
})
export class AppModule { }
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## 컴포넌트 등록 및 사용

이로서 설치부터 설정까지 마무리 되었으니 프로젝트에 필요한 컴포넌트 모듈을 불러온 후, 사용하면 됩니다. [Checkbox 컴포넌트](https://material.angular.io/components/checkbox/overview)를 불러와 적용하는 방법을 공부해봅니다.

모든 컴포넌트에서 Checkbox 컴포넌트를 사용하기 위해 `MatCheckboxModule`를 `@NgModule` 모듈 `imports` 항목에 추가합니다.

{% code-tabs %}
{% code-tabs-item title="src/app.modules.ts" %}
```typescript
import {MatCheckboxModule} from '@angular/material';

@NgModule({
  ...
  imports: [
    BrowserModule,
    BrowserAnimationsModule,
    MatCheckboxModule,
  ],
  ...
})
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Checkbox 컴포넌트를 등록했으니 이어서 컴포넌트 템플릿 파일에서 사용하는 예를 살펴보겠습니다. 사용 방법은 간단합니다.

{% code-tabs %}
{% code-tabs-item title="HTML" %}
```markup
<mat-checkbox>Angular Material 사용에 동의합니다.</mat-checkbox>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## 테마 설정

애플리케이션에 사용할 Material 테마 스타일을 설정할 수 있습니다. Angular 팀에서 사전에 준비한 테마로 시작하려면 `src/style.css` 파일에 다음과 같이 코드를 추가합니다. Angular 팀에서 준비한 기본 테마는 4가지 입니다.

* deeppurple-amber.css
* indigo-pink.css
* pink-bluegrey.css
* purple-green.css

{% code-tabs %}
{% code-tabs-item title="src/style.css" %}
```css
@import "~@angular/material/prebuilt-themes/deeppurple-amber.css";
```
{% endcode-tabs-item %}
{% endcode-tabs %}

직접 테마 파일을 로드하길 선호한다면 `src/index.html` 파일 `<head>` 영역에 다음과 같은 코드를 추가할 수도 있습니다.

{% code-tabs %}
{% code-tabs-item title="src/index.html" %}
```markup
<link
  href="node_modules/@angular/material/prebuilt-themes/indigo-pink.css" 
  rel="stylesheet">
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% hint style="info" %}
Angular 팀에서 만든 테마가 아니라 직접 테마를 제작하려면 [테마 가이드](https://material.angular.io/guide/theming)를 참고해 작성합니다.
{% endhint %}

## 제스처 라이브러리 설정

일부 Material 컴포넌트\(`mat-slide-toggle`, `mat-slider`, `matTooltip`\)는 [HammerJS](http://hammerjs.github.io/) 제스처\(gesture\) 라이브러리에 의존합니다. 컴포넌트가 정상 작동하려면 라이브러리를 로드해야 합니다.

컴포넌트를 문제없이 사용하기 위해 HammerJS 라이브러리를 설치합니다.

```bash
$ npm i hammerjs
```

이어서 애플리케이션 엔트리 포인트인 `src/main.ts` 파일에 HammerJS 라이브러리를 불러오면 문제없이 제스처 라이브러리에 의존하는 컴포넌트를 사용할 수 있습니다.

{% code-tabs %}
{% code-tabs-item title="src/main.ts" %}
```typescript
import 'hammerjs';
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## Material 아이콘 설정 \(옵션\)

공식 [Material 디자인 아이콘](https://material.io/tools/icons/)을 프로젝트에 사용하고자 한다면 아이콘 폰트를 로드합니다.

{% code-tabs %}
{% code-tabs-item title="src/index.html" %}
```markup
<link
  href="https://fonts.googleapis.com/icon?family=Material+Icons"
  rel="stylesheet">
```
{% endcode-tabs-item %}
{% endcode-tabs %}

사용 방법은 다음과 같습니다. 콘텐츠로 추가되는 텍스트에 따라 아이콘이 변경됩니다. 설정 가능한 아이콘 식별 텍스트는 [Material 디자인 아이콘](https://material.io/tools/icons/)를 확인할 수 있습니다.

{% code-tabs %}
{% code-tabs-item title="HTML" %}
```markup
<i class="material-icons" aria-hidden="true">home</i>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% hint style="info" %}
보다 자세한 사용 방법은 [Material 아이콘 가이드](https://google.github.io/material-design-icons/)를 참고하세요.
{% endhint %}

## 사용 예시

### Form Field + Input

[Form field](https://material.angular.io/components/form-field/overview), [Input](https://material.angular.io/components/input/overview) 폼 컴포넌트를 사용하기 위해서는 먼저 각 모듈을 호출해야 합니다.

{% code-tabs %}
{% code-tabs-item title="app.module.ts" %}
```typescript
import { MatFormFieldModule } from '@angular/material/form-field';
import { MatInputModule }     from '@angular/material/input';

@NgModule({
  imports: [
    MatFormFieldModule,
    MatInputModule
  ]
});

```
{% endcode-tabs-item %}

{% code-tabs-item title="component.html" %}
```markup
<form>
  <mat-form-field>
    <label class="a11y-hidden" for="passport-id">패스포트 ID</label>
    <input 
      mat-input 
      id="passport-id"
      type="text"
      placeholder="패스포트 ID">
  </mat-form-field>
</form>
```
{% endcode-tabs-item %}

{% code-tabs-item title="component.css" %}
```css
.a11y-hidden {
  overflow: hidden;
  position: absolute;
  clip: rect(0,0,0,0);
  width: 1px;
  height: 1px;
  margin: -1px;
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

![Angular Material &#xD328;&#xC2A4;&#xD3EC;&#xD2B8; ID &#xD3FC; &#xC785;&#xB825; &#xD544;&#xB4DC;](../.gitbook/assets/image%20%2812%29.png)

### Button + Icon

{% code-tabs %}
{% code-tabs-item title="app.module.ts" %}
```typescript
import { MatButtonModule } from '@angular/material/button';
import { MatIconModule }   from '@angular/material/icon';

@NgModule({
  imports: [
    MatButtonModule,
    MatIconModule
  ]
});
```
{% endcode-tabs-item %}

{% code-tabs-item title="component.html" %}
```markup
<div class="button-group" role="group">
  <button mat-icon-button color="primary">
    <mat-icon aria-label="좋아요">favorite</mat-icon> 
  </button>
  <span>{{ count }}</span>
</div>
```
{% endcode-tabs-item %}

{% code-tabs-item title="component.css" %}
```css
[mat-icon-button] + span {
  margin-left: 0.1em; 
  vertical-align: -2px; 
  color: #8a2be2;
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

![Angular Material &#xC544;&#xC774;&#xCF58; &#xBC84;&#xD2BC;](../.gitbook/assets/image%20%282%29.png)



