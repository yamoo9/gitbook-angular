# HttpClient 모듈

### HTTPClientModule 임포트

Angular 프레임워크 컴포넌트 또는 서비스에서 비동기 통신 하려면 [HttpClientModule](https://angular.io/api/common/http/HttpClientModule)을 `app.module.ts`에 불러와 `@NgModule`에 임포트 합니다.

{% code-tabs %}
{% code-tabs-item title="app.module.ts" %}
```typescript
import { HttpClientModule } from '@angular/common/http';

@NgModule({
  // ...
  imports: [
    // ...
    HttpClientModule
  ],
  // ...
})
export class AppModule {}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### HTTPClient 임포트

Angular 서비스 또는 컴포넌트에 [HttpClient](https://angular.io/api/common/http/HttpClient) 모듈을 불러온 후, 의존성 주입\([DI](https://angular.io/guide/dependency-injection), Dependency Injection\) 합니다.

{% code-tabs %}
{% code-tabs-item title="colors.service.ts" %}
```typescript
import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';

@Injectable({
  provideIn: 'root'
})
exprt class ColorsService {
  // 의존성 모듈 주입
  constructor( private http:HttpClient ) {}
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### 서비스를 사용하는 이유

개별 컴포넌트 마다 직접 HTTP 통신 요청을 하면 관리하거나, 테스트 하기 어려워 집니다. 반면 서비스를 사용해 HTTP 통신 과정을 캡슐화 하여 사용하면 관리하기가 매우 용이하기 때문입니다.

### 데이터 생성

프로젝트 `src/assets` 디렉토리에 통신할 데이터 파일을 생성합니다.

{% code-tabs %}
{% code-tabs-item title="colors.json" %}
```javascript
{
  "version": "0.0.2",
  "colors": [
    {
      "id": 1,
      "name": "Arizalin Crimson",
      "code": {
        "rgba": "rgba(225, 49, 55, 1)",
        "hex": "#e13137"
      }
    },
    {
      "id": 2,
      "name": "Bleu De France",
      "code": {
        "rgba": "rgba(68, 138, 255, 1)",
        "hex": "#448aff"
      }
    }
  ]
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### 인터페이스 정의

`src/app/interfaces` 내부에 Color, Colors 인터페이스 파일을 만들어 각 인터페이스를 정의합니다.

{% code-tabs %}
{% code-tabs-item title="color.interface.ts" %}
```typescript
export interface Color {
  id?: number;
  name: string;
  code: {
    rgba: string;
    hex: string;
  }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="colors.interface.ts" %}
```typescript
import { Color } from './color.interface';

export interface Colors {
  version: string;
  colors: Color[];
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### GET : 데이터 읽기

공급된 HttpClient 객체를 참조하는 `this.http` 객체의 `get()` 메서드를 사용해 GET 통신할 수 있습니다.

{% code-tabs %}
{% code-tabs-item title="colors.service.ts" %}
```typescript
import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';
import { Colors }     from '../interface/colors.interface';

@Injectable({
  provideIn: 'root'
})
exprt class ColorsService {
  
  // 에셋 URL
  url:string = 'assets/colors.json';
  
  // 의존성 모듈 HttpClient 주입
  constructor( private http:HttpClient ) {}
  
  requestColors() {
    // GET 통신 ⟹ 데이터 가져오기
    // Colors 인터페이스를 제네릭으로 설정
    return this.http.get<Colors>(this.url);
  }
  
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% hint style="info" %}
JSON이 아닌 다른 포멧 데이터를 통신하고자 할 경우, [옵션 responseType을 설정](https://angular.io/guide/http#requesting-non-json-data)합니다.

```typescript
this.http.get(this.url, { responseType: 'text' });
```
{% endhint %}

컴포넌트는 서비스를 주입 받아, 서비스의 메서드를 사용해 통신 응답 결과를 컴포넌트의 속성에 할당할 수 있습니다.

{% code-tabs %}
{% code-tabs-item title="colors.component.ts" %}
```typescript
import { ColorsService } from '../httpConfig.service';
import { Color }         from '../interfaces/color.interface';

@Component({
  selector: 'app-colors',
  templateUrl: './colors.component.html',
})
export class ColorsComponent {
  
  this.colors:Color[]|null = null;
  
  // colorsService 주입
  constructor(private colorsService:ColorsService) {}
  
  getColors(){
    this.colorsService
      .requestColors()
      // 구독(subscribe) 메서드를 통해 통신 응답 결과를 수신
      .subscribe(res => this.colors = res.colors);
  }
  
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

#### 전체 응답 결과 확인

HttpClient 객체의 `get()` 메서드 사용 시, [`observe` 옵션 설정 값을 `'response'`로 설정](https://angular.io/guide/http#reading-the-full-response)하면 응답\(response\) 결과를 가진 객체를 반환합니다. 사용자가 필요로 하는 정보는 `body` 속성에 담겨 있습니다.

{% code-tabs %}
{% code-tabs-item title="colors.service.ts" %}
```typescript
requestColors() {
  // 모든 응답 결과를 확인하기 위한 observe 설정
  return this.http.get<Colors>(this.url, {observe: 'response'});
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="colors.component.ts" %}
```typescript
getColors(){
  this.colorsService
    .requestColors()
    .subscribe(res => {
      console.group('HTTP 응답 결과');
        console.log(`HEADERS:`, res.headers);
        console.log(`OK: ${res.ok}`);
        console.log(`BODY:`, res.body);
        console.log(`STATUS: ${res.status}`);
        console.log(`TYPE: ${res.type}`);
        console.log(`URL: ${res.url}`); 
        // 헤더(headers) X-Powered-By 속성 가져오기
        // console.log(`Powered: ${res.headers.get('X-Powered-By')}`);
      console.groupEnd();
    });
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

응답 결과는 다음과 같이 콘솔 패널에 출력됩니다.

![&#xC751;&#xB2F5; &#xACB0;&#xACFC; &#xCF58;&#xC194; &#xD328;&#xB110;&#xC5D0; &#xCD9C;&#xB825;](../.gitbook/assets/image%20%2810%29.png)

### POST : 데이터 생성

HttpClient 객체의 `post()` 메서드를 사용해 생성할 데이터를 전달하면 통신을 통해 데이터를 생성할 수 있습니다. 통신 [오류 디버깅 시에는 HttpErrorResponse를 이용](https://angular.io/guide/http#getting-error-details)합니다. `subscribe()` 메서드의 2번째 인자로 오류 콜백 함수를 전달합니다.

{% code-tabs %}
{% code-tabs-item title="colors.service.ts" %}
```typescript
import { HttpClient, HttpErrorResponse } from '@angular/common/http';
import { Color } from '../interfaces/color.interface';

// payload 인자 값의 유형을 Color 인터페이스로 설정
createColor(payload:Color):void {
  this.http.post(this.url, payload).subscribe(
    res => console.log(res),
    (err:HttpErrorResponse) => console.error(error)
  );
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

서비스를 통해 데이터를 생성하는 `createColor()` 메서드는 컴포넌트에 작성합니다.

{% code-tabs %}
{% code-tabs-item title="colors.component.ts" %}
```typescript
createColor():void {
  // 서비스 객체의 createColor() 메서드에 Color 객체 전달
  // 서버 통신 후, 성공하면 데이터 추가
  this.colorsService.createColor({
    name: 'black',
    code: {
      rgba: 'rgba(0,0,0,1)',
      hex: '#000'
    }
  });
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### PUT : 데이터 업데이트

HttpClient 객체의 `put()` 메서드를 사용해 수정할 데이터 식별자와 데이터를 전달하면 통신을 통해 데이터를 수정할 수 있습니다. 매개변수 옵션을 설정할 겨우 HttpParams 클래스를 필요로 합니다.

{% code-tabs %}
{% code-tabs-item title="colors.service.ts" %}
```typescript
import { HttpClient, HttpErrorResponse, HttpParams } from '@angular/common/http';

updateColor(payload:Color):void {
  this.http.put<Color>(this.url, payload, {
    // 매개변수 옵션 설정 시, HttpParams 객체를 통해 설정
    params: new HttpParams().set('id', '3'),
  })
  .subscribe(
    res => console.log(res),
    (err:HttpErrorResponse) => console.log(err)
  );
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

서비스를 통해 데이터를 생성하는 `updateColor()` 메서드는 컴포넌트에 작성합니다.

{% code-tabs %}
{% code-tabs-item title="colors.component.ts" %}
```typescript
updateColor():void {
  // 서비스 객체의 updateColor() 메서드에 Color 객체 전달
  // 서버 통신 후, 성공하면 데이터 수정
  this.colorsService.updateColor({
    name: 'white',
    code: {
      rgba: 'rgba(255,255,255,1)',
      hex: '#fff'
    }
  });
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% hint style="info" %}
인증\(Authorization\)이 요구될 경우, [HttpHeaders 클래스를 사용해 토큰\(Token\)을 설정](https://angular.io/guide/http#adding-headers)합니다.

```typescript
import { HttpParams, HttpHeaders } from '@angular/common/http';

this.http.put<Color>(this.url, payload, {
  params: new HttpParams().set('id', '3'),
  // 접근 권한이 필요한 경우: 토큰 정보를 추가합니다.
  headers: new HttpHeaders().set('Authorization', 'Token ....'),
})
```
{% endhint %}

### DELETE : 데이터 제거

HttpClient 객체의 `delete()` 메서드를 사용해 제거할 식별자를 전달하면 통신을 통해 데이터를 제거할 수 있습니다.

{% code-tabs %}
{% code-tabs-item title="colors.service.ts" %}
```typescript
deleteColor(id:number):void {
  const url:string = `${this.url}/${id}`;
  this.http.delete(url, payload);
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

서비스를 통해 데이터를 생성하는 `deleteColor()` 메서드는 컴포넌트에 작성합니다.

{% code-tabs %}
{% code-tabs-item title="colors.component.ts" %}
```typescript
deleteColor():void {
  this.colorsService.deleteColor(3).subscribe(
    res => console.log(res),
    (err:HttpErrorResponse) => console.log(err)
  );
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

