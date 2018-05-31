# 프로젝트 파일 구조

## 파일 구조\(File Structure\)

Angular CLI 도구를 통해 생성된 프로젝트 구조에서 먼저 살펴 볼 부분은 정리해봅니다.

{% code-tabs %}
{% code-tabs-item title="Angular 프로젝트 구조" %}
```bash
.
├── README.md
├── angular.json
├── e2e/
├── node_modules/
├── package-lock.json
├── package.json
├── src/
│   ├── app/
│   │   ├── app.component.css
│   │   ├── app.component.html
│   │   ├── app.component.spec.ts
│   │   ├── app.component.ts ⬅⬅⬅
│   │   └── app.module.ts  ⬅⬅⬅
│   ├── assets/
│   ├── browserslist
│   ├── environments/
│   │   ├── environment.prod.ts
│   │   └── environment.ts
│   ├── favicon.ico
│   ├── index.html  ⬅⬅⬅
│   ├── karma.conf.js
│   ├── main.ts  ⬅⬅⬅
│   ├── polyfills.ts
│   ├── styles.css
│   ├── test.ts
│   ├── tsconfig.app.json
│   ├── tsconfig.spec.json
│   └── tslint.json
├── tsconfig.json
└── tslint.json
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## Angular 프로젝트 소스\(`src`\) 디렉토리

| 파일 | 용도 |
| --- | --- |
| `app/app.component.{ts,html,css,spec.ts}` | AppComponent 컴포넌트를 구성하는 HTML 템플릿 파일, CSS 스타일 파일, 유닛 테스트\(`spec`\) 파일 |
| `app/app.module.ts` | Angular 애플리케이션의 AppModule 루트 모듈 정의 \(모듈 추가 사용\) |
| `assets/*` | 애플리케이션 빌드 시, 이미지와 같은 에셋을 보관하는 디렉토리 |
| `environments/*` | 빌드 환경 구성 변수를 포함한 파일들이 포함된 디렉토리 |
| `browserslist` | 브라우저 호환 범위를 설정하는 구성 파일 |
| `favicon.ico` | 파비콘 \(Favorite Icon\), PNG 파일도 사용 가능 |
| `index.html` | 사용자에게 보여지는 인덱스 HTML 페이지 |
| `karma.conf.js` | Karma 유닛 테스트 구성 파일로 `ng test` 명령 입력 시 실행 |
| `main.ts` | 애플리케이션 엔트리 포인트. JIT 컴파일러로 애플리케이션 루트 모듈\(`AppModule`\)을 부트스트래핑하여 브라우저에서 실행 |
| `polyfills.ts` | 브라우저마다 웹 표준 지원 수준이 달라, 이러한 차이를 표준화 처리. [Browser Support](https://angular.io/guide/browser-support) 참고 |
| `styles.css` | 글로벌 스타일 파일 \(모든 컴포넌트에 영향\) |
| `test.ts` | 유닛 테스트의 엔트리 포인트 |
| `tsconfig.{app,spec}.json` | Angular 애플리케이션\(`tsconfig.app.json`\), 유닛 테스트\(`tsconfig.spec.json`\)에 대한 TypeScript 컴파일러 구성 파일 |
| `tslint.json` | 코드 스타일을 일관성있게 유지하기 위한 구성 파일 |

## Angular 프로젝트 루트\(`root`\) 디렉토리

| 파일 | 용도 |
| --- | --- |
| `e2e/` | End to End 테스트를 수행과 관련된 것들이 포함된 디렉토리 |
| `node_modules/` | Node.js 개발 모듈이 포함된 디렉토리 |
| `.editorconfig` | 프로젝트를 사용하는 팀원 모두가 공통된 구성을 가지도록 에디터 설정을 일관화하는 구성 파일. [editorconfig.org](http://editorconfig.org/) 참고 |
| `.gitignore` | Git 버전 관리 시스템에서 관리를 제외할 항목을 관리하는 파일 |
| `angular.json` | Angular CLI 구성 파일 |
| `package.json` | Node.js 개발 모듈 및 사용자 정의 NPM 스크립트를 관리하는 파일 |
| `protractor.conf.js` | Angular End to End 테스트 시에 사용되는 파일 `ng e2e` |
| `README.md` | Angular CLI 명령어 목록을 포함한 프로젝트 기본 문서 |
| `tsconfig.json` | 사용자 에디터에서 픽업하여 유용한 툴링을 제공하는 TypeScript 컴파일러 구성 파일 |
| `tslint.json` | 코드 스타일을 일관성있게 유지하기 위한 구성 파일 |



보다 자세한 내용은 [Angular - QuickStart](https://angular.io/guide/quickstart)를 참고하세요.

