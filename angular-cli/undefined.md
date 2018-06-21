# 외부 모듈

## 외부 모듈 등록

Angular의 빌드 시스템은 애플리케이션에서 사용하는 모든 파일을 알고 있기에 프로세스를 간소화 할 수 있습니다. 하지만 Angular가 애플리케이션에 사용된 파일 중 일부를 모른다면? 해당 파일은 빌드 될 때 포함되지 않아 문제가 발생할 것입니다. 외부 모듈을 애플리케이션 개발에 사용했다면 Angular가 이를 알 수 있도록 조치해야 빌드 시 문제가 발생하지 않습니다.

### 로컬 설치 모듈

만약 [moment.js](https://momentjs.com/) 외부 모듈을 프로젝트에 사용하고자 한다면 먼저 모듈을 설치합니다. Angular는 TypeScript를 사용하기에 유형 정의 파일 또한 함께 설치해줍니다. 로컬 설치 모듈의 경우, Angular 빌드 시스템이 자동으로 포함해 빌드 프로세싱 합니다.

```bash
$ npm i moment @types/moment
```

![&#xB0A0;&#xC9DC;\(Date\)&#xD615;&#xC2DD; &#xB370;&#xC774;&#xD130; &#xD30C;&#xC2F1;, &#xAC80;&#xC99D;, &#xC870;&#xC791;, &#xD654;&#xBA74;&#xC5D0; &#xCD9C;&#xB825;&#xD558;&#xB294; &#xB77C;&#xC774;&#xBE0C;&#xB7EC;&#xB9AC;](../.gitbook/assets/image%20%284%29.png)

moment.js 모듈을 Angular 파일\(ts\)에서 불러와 사용하는 예시 코드는 다음과 같습니다.

{% code-tabs %}
{% code-tabs-item title="angular.file.ts" %}
```typescript
import * as moment from 'moment';

moment().format('MMMM Do YYYY, h:mm:ss a'); // 6월 21일 2018, 11:33:23 오전 
moment().format('dddd');                    // 목요일 
moment().format("MMM Do YY");               // 6월 21일 18 
moment().format('YYYY [escaped] YYYY');     // 2018 escaped 2018 
moment().format();                          // 2018-06-21T11:33:23+09:00
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% hint style="info" %}
moment.js의 자세한 사용법은 [moment.js](https://momentjs.com/docs) 문서를 살펴보시길 바랍니다.
{% endhint %}

### 글로벌 설치 모듈

때때로 프로젝트 내부에 설치하지 않은 모듈을 사용해야 할 경우가 있습니다. 이런 경우 Angular 빌드 프로세스에 포함되어 빌드 되지 않기 때문에 사용자가 직접 `angular.json` 파일을 열어 글로벌 모듈을 등록해야 합니다.

만약 Bootstrap과 jQuery를 Angular 프로젝트에 사용하고자 한다면 다음과 같이 설치를 먼저 수행합니다.

```bash
# Bootstrap은 jQuery 라이브러리에 의존하기 때문에 함께 설치됩니다.
# 하지만 jQuery 라이브러리 TypeScript 유형 정의 파일은 별도로 설치해야 합니다.
$ npm i bootstrap @types/jquery
```

이어서 `angular.json` 파일에 설치한 모듈을 포함해야 합니다. `styles`, `scripts` 배열에 `node_modules` 디레토리에 있는 Bootstrap, jQuery 파일 경로를 포함 시킵니다.

{% code-tabs %}
{% code-tabs-item title="angular.json" %}
```javascript
{
  ...
  "architect": {
    ...
    "build": {
      ...
      "options": {
        ...
        "styles": [ 
          "node_modules/bootstrap/dist/css/bootstrap.min.css", 
          "src/styles.css" 
        ],
        "scripts": [ 
          "node_modules/jquery/dist/jquery.slim.min.js",
          "node_modules/bootstrap/dist/bootstrap.min.js" 
        ]
      }
      ...
    }
  }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

jQuery 모듈을 TypeScript 파일에 불러와 사용하는 방법은 다음과 같습니다.

{% code-tabs %}
{% code-tabs-item title="angular.file.ts" %}
```typescript
import * as $ from 'jquery';

$(document).ready($ => console.log($.fn.jquery));
```
{% endcode-tabs-item %}
{% endcode-tabs %}

![DOM\(&#xBB38;&#xC11C; &#xAC1D;&#xCCB4; &#xBAA8;&#xB378;\) &#xC870;&#xC791;&#xC5D0; &#xD0C1;&#xC6D4;&#xD55C; jQuery &#xB77C;&#xC774;&#xBE0C;&#xB7EC;&#xB9AC;](../.gitbook/assets/image%20%282%29.png)

{% hint style="info" %}
추가적으로 Angular CLI에 대한 자세한 사용법은 [Angular CLI](https://github.com/angular/angular-cli/wiki) Wiki를 참고해보세요.
{% endhint %}

