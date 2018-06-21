# 신규

## 프로젝트 생성

`ng new` 명령어 뒤에 `<프로젝트-이름>` 입력 후 실행합니다. 개발에 필요한 의존 모듈들을 다운로드 받기 때문에 적지 않은 시간이 소요됩니다. 의존 모듈을 설치하지 않고 프로젝트 스케폴딩 하길 원한다면 `--skip-install` 옵션을 추가해 설치합니다.

```bash
# ng new <프로젝트-이름>
$ ng new ng6project

# 의존 모듈을 설치하지 않고 스캐폴딩
$ ng new ng6project --skip-install

# app(기본)이 아닌, 프로젝트 접두사(-p) 설정
$ ng new ng6project --prefix <프로젝트-접두사>

# 유닛 테스트 제외(-S) 설정
$ ng new ng6project --skip-tests

# Git 버전관리 제외(-g) 설정
$ ng new ng6project --skip-git
```

생성된 프로젝트 스캐폴딩 구조는 다음과 같습니다. 이와 같은 구조와 코딩 컨벤션이 **Angular 프레임워크 프로젝트의 표준 구조**입니다.

{% code-tabs %}
{% code-tabs-item title="프로젝트 파일 구조" %}
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
│   │   ├── app.component.ts
│   │   └── app.module.ts
│   ├── assets/
│   ├── browserslist
│   ├── environments/
│   │   ├── environment.prod.ts
│   │   └── environment.ts
│   ├── favicon.ico
│   ├── index.html
│   ├── karma.conf.js
│   ├── main.ts
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

## 프로젝트 버전 정보

프로젝트 디렉토리 위치에서 버전 출력 명령을 실행해보면 프로젝트에 설치된 패키지 정보를 확인할 수 있습니다.

```bash
# ng6project 디렉토리로 이동
$ cd ng6project

# 프로젝트 버전 출력
$ ng -v
```

{% code-tabs %}
{% code-tabs-item title="프로젝트 버전 출력 화면" %}
```bash
     _                      _                 ____ _     ___
    / \   _ __   __ _ _   _| | __ _ _ __     / ___| |   |_ _|
   / △ \ | '_ \ / _` | | | | |/ _` | '__|   | |   | |    | |
  / ___ \| | | | (_| | |_| | | (_| | |      | |___| |___ | |
 /_/   \_\_| |_|\__, |\__,_|_|\__,_|_|       \____|_____|___|
                |___/


Angular CLI: 6.0.5
Node: 8.11.1
OS: darwin x64
Angular: 6.0.3
... animations, common, compiler, compiler-cli, core, forms
... http, language-service, platform-browser
... platform-browser-dynamic, router

Package                           Version
-----------------------------------------------------------
@angular-devkit/architect         0.6.5
@angular-devkit/build-angular     0.6.5
@angular-devkit/build-optimizer   0.6.5
@angular-devkit/core              0.6.5
@angular-devkit/schematics        0.6.5
@angular/cli                      6.0.5
@ngtools/webpack                  6.0.5
@schematics/angular               0.6.5
@schematics/update                0.6.5
rxjs                              6.2.0
typescript                        2.7.2
webpack                           4.8.3
```
{% endcode-tabs-item %}
{% endcode-tabs %}



