# 데이터 쓰기 / 갱신 / 제거

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

{% hint style="info" %}
데이터 중 일부만 수정 하려면 PUT 대신 PATCH 메서드를 사용할 수 있습니다.

```typescript
this.http.patch(...).subscribe(...)
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

