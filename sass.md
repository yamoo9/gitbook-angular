# Sass 프리프로세서 \(옵션\)

### Sass 프리프로세서 사용 설정

Angular CLI 명령어를 사용해 프로젝트 생성 시, `--style` 옵션을 사용해 `sass`, `scss` 중 Sass 문법을 선택해 사용할 수 있습니다.

{% code-tabs %}
{% code-tabs-item title="Angular CLI" %}
```bash
# Angular CLI 명령어 --style 옵션(sass,scss)
$ ng new <프로젝트-이름> --style sass
```
{% endcode-tabs-item %}
{% endcode-tabs %}

생성된 프로젝트는 옵션을 통해 설정한 Sass 문법에 맞는 파일을 확인할 수 있습니다.

{% code-tabs %}
{% code-tabs-item title="Project Root" %}
```bash
# styles.css 대신 styles.sass 파일이 생성됨
src/ 
└── styles.sass
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### Sass 프리프로세서 옵션 설정

`angular.json` 파일을 열어 Angular 컴포넌트 스타일 파일에서 호출할 수 있도록 `stylePreprocessorOptions` 옵션을 추가합니다. 

{% code-tabs %}
{% code-tabs-item title="angular.json" %}
```javascript
{
  "projects": {
    "angular-project": {
      "architect": {
        "build": {
          "options": {
            // ...
            "styles": [ "src/styles.sass" ], 
            "stylePreprocessorOptions": { 
              "includePaths": ["src/"] 
            },
            // ...
          }
        }
      }
    }
  }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

유닛 테스트를 사용한다면 `test` 내부에도 `stylePreprocessorOptions` 를 추가합니다.

{% code-tabs %}
{% code-tabs-item title="angular.json" %}
```javascript
{
  "projects": {
    "angular-project": {
      "architect": {
        // ...
        "test": {
          "options": {
            // ...
            "styles": [ "src/styles.sass" ], 
            "stylePreprocessorOptions": { 
              "includePaths": ["src/"] 
            },
            // ...
          }
        }
      }
    }
  }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### Sass 공통 변수/믹스인 구성

src 디렉토리 내부에 sass 디렉토리를 생성한 후, 변수/믹스인/메인 Sass 파일을 생성합니다.

{% code-tabs %}
{% code-tabs-item title="Project Root" %}
```bash
src/ 
├── app/
├── assets/
├── index.html 
# src 내부에 sass 디렉토리를 만든 후, Sass 변수, 믹스인, 메인 파일을 생성
└── sass/ 
  ├── _mixins.sass 
  ├── _variables.sass 
  └── main.sass 
```
{% endcode-tabs-item %}
{% endcode-tabs %}

#### main.sass 파일 구성

variables, mixins 등 Sass 모듈 파일을 호출하는 코드를 작성합니다.

{% code-tabs %}
{% code-tabs-item title="src/sass/main.sass" %}
```css
@import "./variables"
@import "./mixins"
```
{% endcode-tabs-item %}
{% endcode-tabs %}

#### \_variables.scss 파일

Sass 변수 파일에는 애플리케이션 전체에서 활용할 공통 변수를 설정합니다.

{% code-tabs %}
{% code-tabs-item title="src/sass/\_variables.scss" %}
```css
$container: ( 
  width: 960px, 
  padding: 10px 
);
```
{% endcode-tabs-item %}
{% endcode-tabs %}

#### \_mixins.scss 파일

Sass 믹스인 파일에는 애플리케이션 전체에서 활용할 공통 믹스인을 설정합니다.

{% code-tabs %}
{% code-tabs-item title="src/sass/\_mixins.scss" %}
```css
=size($width: null, $height: null) 
  width: $width 
  height: $height
```
{% endcode-tabs-item %}
{% endcode-tabs %}

#### 컴포넌트.sass 파일

Angular 컴포넌트 스타일 파일에서 `sass/main.sass` 파일을 로드 하면 Sass 변수, 믹스인을 사용할 수 있습니다.

```css
@import "./sass/main"

.container
  $w: map-get($container, width)
  +size($w, auto)
```

