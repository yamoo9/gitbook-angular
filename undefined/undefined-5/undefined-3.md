# 양방향 데이터 바인딩

양방향 바인딩은 `ngModel` 디렉티브를 사용하여 이벤트 바인딩 및 속성 바인딩을 동시에 처리합니다. Angular CLI는 기본적으로 양방향 바인딩을 사용할 수 있도록 구성하지 않습니다. 사용자는 양방향 바인딩을 사용하기 위해 다음의 설정을 수행해야 합니다.

## FormsModule 로드 & 임포트

`FormsModule`을 `@angular/forms`로 부터 로드한 후에 `@NgModule`의 `imports` 항목에 추가해야 양방향 바인딩을 사용할 수 있습니다.

```typescript
// app/app.module.ts

/** Modules */
import { BrowserModule }  from '@angular/platform-browser';
import { NgModule }       from '@angular/core';

// FormsModule을 로드
import { FormsModule }    from "@angular/forms";

/** Components */
import { AppComponent }    from './app.component';
import { ButtonComponent } from "./button/button.component";
import { InputComponent }  from "./input/input.component";


@NgModule({
  declarations: [
    AppComponent,
    ButtonComponent,
    InputComponent,
  ],
  imports: [
    BrowserModule,
    // FormsModule 모듈을 imports에 등록
    FormsModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

## ngModel 디렉티브

Angular는 `ngModel` 디렉티브를 통해 양방향 바인딩\(`[()]`\)을 간단하게 처리할 수 있습니다.

**TypeScript**

```typescript
// app/input/input.component.ts

...

@Component(metadata)
export class InputComponent {

  public label_id:            string = 'y9-username';
  public label_conetnt:       string = '사용자 이름';
  public type:                string = 'text';
  private pass_by_user_input: string = '';

}
```

클래스에 설정된 비공개 속성 `pass_by_user_input`를 템플릿 `<input>` 요소 마크업에 `[(ngModel)]` 속성 값으로 설정하면 양방향 바인딩이 됩니다.

**HTML**

```markup
<!-- app/input/input.component.html -->

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
    [(ngModel)]="pass_by_user_input">
</div>

<!-- 사용자 입력 내용 출력 -->
<p class="lead">
  사용자 입력 내용: <b>{{ pass_by_user_input }}</b>
</p>
```

> **NOTE.**  
>  안타깝게도 양방향 바인딩 사용 시, 한글을 포함한 유니코드 문자는 입력에 다소 문제가 있습니다.  
>  \(마지막 입력 후 스페이스를 눌러야 온전히 글자가 보이는 현상\)

## 유니코드 문자 양방향 바인딩

양방향 바인딩 시 한글, 일본어, 중국어 같은 유니코드 문자 입력 문제를 해결하려면 이벤트 바인딩과 속성 바인딩을 동시에 사용하면 됩니다. `(input)` 이벤트에 연결된 `onPasssingByUserInput()` 메서드는 사용자의 입력을 컴포넌트에 전달하고, 컴포넌트는 전달받은 값을 `pass_by_user_input`에 할당하면, 다시 컴포넌트 `<input>` 요소는 업데이트 된 `pass_by_user_input` 값을 받아와 화면에 업데이트 합니다.

**TypeScript**

```typescript
// app/input/input.component.ts

...

@Component(metadata)
export class InputComponent {

  public label_id:            string = 'y9-username';
  public label_conetnt:       string = '사용자 이름';
  public type:                string = 'text';
  private pass_by_user_input: string = '';

  // 이벤트 바인딩 메서드
  onPasssingByUserInput($event): void {
    this.pass_by_user_input = $event.target.value;
  }

}
```

**HTML**

```markup
<!-- app/input/input.component.html -->

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
    (input)="onPasssingByUserInput($event)"
    [value]="pass_by_user_input">
</div>

<p class="lead">
  사용자 입력 내용:
  <b>{{ pass_by_user_input }}</b>
</p>
```

