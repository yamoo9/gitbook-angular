# 데이터 읽기

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

