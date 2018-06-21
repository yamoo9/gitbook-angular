# 빌드

## 프로젝트 빌드

프로젝트 개발이 완료되면, 빌드 명령을 통해 웹에 호스팅 할 수 있는 배포 자료를 만듭니다.

```bash
# 빌드
$ ng build
```

배포 자료는 `dist` 디렉토리 생성 후, 내부에 만들어 집니다.

```text
dist 
└── <프로젝트-이름> 
     ├── 3rdpartylicenses.txt 
     ├── favicon.ico 
     ├── index.html 
     ├── main.js 
     ├── main.js.map 
     ├── polyfills.js 
     ├── polyfills.js.map 
     ├── runtime.js 
     ├── runtime.js.map 
     ├── styles.js
     ├── styles.js.map 
     ├── vendor.js 
     └── vendor.js.map
```

빌드 된 자료를 로컬 테스트 서버로 구동하면 Angular 애플리케이션이 구동됩니다. 별도로 사용 중인 테스트 서버 모듈이 없다면 [live-server](https://www.npmjs.com/package/live-server) 설치 후, 다음과 같이 명령을 입력합니다.

```bash
$ live-server dist/<프로젝트-이름>
```

{% hint style="info" %}
live-server 외에도 사용 가능한 개발 모듈을 설치해 사용할 수 있습니다.

* [http-server](https://www.npmjs.com/package/http-server)
* [lite-server](https://www.npmjs.com/package/lite-server)
{% endhint %}

## 프로젝트 배포 빌드

앞서 다룬 빌드 명령은 코드 최적화가 이루어지지는 않습니다. 코드를 최적화 한 빌드를 수행하려면 `--prod` 옵션을 추가해 실행해야 합니다. 코드 최적화를 위해 `uglify`, `tree-shaking`이 수행됩니다.

```bash
# 배포 빌드(코드 최적화)
$ ng build --prod
```

`--prod` 옵션을 추가해 실행한 빌드 결과는 다음과 같습니다. 최적화되어 각 파일 크기가 작아졌고, 브라우저 캐시 무효화를 위한 임의의 문자열이 접미사로 추가되었습니다. 캐시가 무효화되었기에 이전의 캐시 된 파일을 사용하지 않고, 새로운 버전의 파일을 다운로드 받습니다.

```text
dist 
└── <프로젝트-이름>  
     ├── 3rdpartylicenses.txt 
     ├── favicon.ico 
     ├── index.html 
     ├── main.40da80692f280989728d.js
     ├── polyfills.7a0e6866a34e280f48e7.js 
     ├── runtime.a66f828dca56eeb90e02.js 
     └── styles.ca60c8bdb366c68153e1.css
```

