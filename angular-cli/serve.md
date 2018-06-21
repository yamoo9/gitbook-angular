# 개발

## 프로젝트 개발

Angular 라이브 개발 서버\(`localhost:4200`\)가 실행됩니다. 기본 웹 브라우저로 바로 실행시키려면 `--open` 옵션을 명령에 추가합니다. 라이브 개발 서버가 실행된 이후, 소스 파일을 수정/저장하면 자동으로 애플리케이션 페이지가 새로고침 됩니다.

```bash
# 라이브 개발 서버 구동
# http://localhost:4200/
$ ng serve

# 라이브 개발 서버 구동 후, 기본 웹 브라우저로 바로 실행
# ng serve --open
$ ng serve -o
```

{% code-tabs %}
{% code-tabs-item title="라이브 개발 서버 구동 화면" %}
```bash
** Angular Live Development Server is listening on localhost:4200, 
   open your browser on http://localhost:4200/ **

Date: 2018-03-21T01:55:17.246Z
Hash: 858b7f2d0c859f625db8
Time: 9050ms
chunk {main} main.js, main.js.map (main) 10.7 kB [initial] [rendered]
chunk {polyfills} polyfills.js, polyfills.js.map (polyfills) 227 kB [initial] [rendered]
chunk {runtime} runtime.js, runtime.js.map (runtime) 5.22 kB [entry] [rendered]
chunk {styles} styles.js, styles.js.map (styles) 15.6 kB [initial] [rendered]
chunk {vendor} vendor.js, vendor.js.map (vendor) 3.39 MB [initial] [rendered]
ℹ ｢wdm｣: Compiled successfully.
```
{% endcode-tabs-item %}
{% endcode-tabs %}

