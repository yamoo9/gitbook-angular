# 설치

## Angular CLI 설치

Angular CLI를 설치하기 위해 다음 명령을 입력합니다. [Node.js](https://nodejs.org), [NPM](https://npmjs.com) 등이 운영체제에 설치되어 있어야 합니다.

```bash
$ npm i -g @angular/cli
```

## Angular CLI 버전 정보

`ng` 명령어 뒤에 `-v` 옵션을 붙여 실행하면, Angular 버전 정보가 출력됩니다.

```bash
# ng --version
$ ng -v
```

{% code-tabs %}
{% code-tabs-item title="설치 결과 화면" %}
```bash
     _                      _                 ____ _     ___
    / \   _ __   __ _ _   _| | __ _ _ __     / ___| |   |_ _|
   / △ \ | '_ \ / _` | | | | |/ _` | '__|   | |   | |    | |
  / ___ \| | | | (_| | |_| | | (_| | |      | |___| |___ | |
 /_/   \_\_| |_|\__, |\__,_|_|\__,_|_|       \____|_____|___|
                |___/


Angular CLI: 6.0.0
Node: 8.11.1
OS: darwin x64
Angular:
...

Package                      Version
------------------------------------------------------
@angular-devkit/architect    0.6.0
@angular-devkit/core         0.6.0
@angular-devkit/schematics   0.6.0
@schematics/angular          0.6.0
@schematics/update           0.6.0
rxjs                         6.1.0
typescript                   2.7.2
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## Angular CLI 도움말

`ng` 명령어 뒤에 `-h` 옵션을 붙여 실행합니다. 사용 가능한 명령 목록을 확인할 수 있습니다.

```bash
# ng --help
$ ng -h
```

{% code-tabs %}
{% code-tabs-item title="사용 가능항 명령 출력 화면" %}
```text
사용 가능한 명령:
  add         라이브러리를 프로젝트에 추가
  new         새로운 디렉토리에 신규 angular 프로젝트 생성
  generate    설계도(schematic)를 기반을 파일을 생성/수정
  update      애플리케이션, 의존성 모듈 업데이트
  build       아웃풋(기본 값: dist) 경로에 앱을 빌드
  serve       파일 변경 시, 앱을 빌드하고 서브(serve)
  test        유닛 테스트 실행
  e2e         e2e 테스트 실행
  lint        코드 린트 수행
  xi18n       소스 코드에서 i18n 메시지 추출
  run         설계 타겟(Architect targets)을 실행
  eject       일시적으로 중지
  config      구성(configuration) 값을 읽고 쓰기
  help        도움말
  version     Angular CLI 버전 출력
  doc         키워드로 공식 Angular API 문서 열기

각 명령 사용에 대한 자세한 도움말은 "ng [command name] --help" 코드를 통해 살펴보세요.
```
{% endcode-tabs-item %}
{% endcode-tabs %}



