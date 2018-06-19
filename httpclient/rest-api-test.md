# REST API 테스트 환경

데이터 읽기에 이어 쓰기/갱신/제거를 테스트 하려면 REST API 테스트 환경이 필요합니다. 간단하게 온라인 REST API 서비스 또는 로컬 REST API 서버를 이용해 볼 수 있습니다.

### REST API 테스트 도구 {#postman}

{% embed data="{\"url\":\"https://www.getpostman.com/\",\"type\":\"link\",\"title\":\"Postman\",\"description\":\"Postman is the only complete API development environment, for API developers, used by more than 5 million developers and 100,000 companies worldwide. Postman makes working with APIs faster and easier by supporting developers at every stage of their workflow, and is available for Mac OS X, Windows, and Linux users.\",\"icon\":{\"type\":\"icon\",\"url\":\"https://www.getpostman.com/img/touch-icons/touch-icon-192x192.png\",\"width\":192,\"height\":192,\"aspectRatio\":1},\"thumbnail\":{\"type\":\"thumbnail\",\"url\":\"https://www.getpostman.com/img/v2/logo-glyph.png\",\"width\":404,\"height\":404,\"aspectRatio\":1}}" %}

![Postman](../.gitbook/assets/image%20%2817%29.png)

### 랜덤 데이터 생성 {#generate-random-data}

{% embed data="{\"url\":\"https://mockaroo.com/\",\"type\":\"link\",\"title\":\"Mockaroo  - Random Data Generator and API Mocking Tool \| JSON / CSV / SQL / Excel\",\"description\":\"A free test data generator and API mocking tool - Mockaroo lets you create custom CSV, JSON, SQL, and Excel datasets to test and demo your software.\",\"icon\":{\"type\":\"icon\",\"url\":\"https://mockaroo.com/assets/favicon-8d320ac46812befcc8e0c5388550bd14d2105f78bb354728e63dd50d9e345ede.png\",\"aspectRatio\":0}}" %}

{% embed data="{\"url\":\"https://randomuser.me/\",\"type\":\"link\",\"title\":\"Random User Generator \| Home\",\"description\":\"Random user generator is a FREE API for generating placeholder user information. Get profile photos, names, and more. It\'s like Lorem Ipsum, for people.\",\"icon\":{\"type\":\"icon\",\"url\":\"https://randomuser.me/favicon.ico\",\"aspectRatio\":0}}" %}

{% embed data="{\"url\":\"http://www.designskilz.com/random-users/\",\"type\":\"link\",\"title\":\"Generate fake users for your UI mockups\",\"description\":\"Generate fake users for your UI mockups. This is a simple web tool to help you generate random and fake users to use in your projects.\",\"icon\":{\"type\":\"icon\",\"url\":\"http://www.designskilz.com/random-users/favicon.ico\",\"aspectRatio\":0},\"thumbnail\":{\"type\":\"thumbnail\",\"url\":\"http://www.designskilz.com/random-users/share.jpg\",\"width\":800,\"height\":500,\"aspectRatio\":0.625}}" %}

{% embed data="{\"url\":\"https://github.com/marak/Faker.js/\",\"type\":\"link\",\"title\":\"Marak/faker.js\",\"description\":\"faker.js - generate massive amounts of fake data in Node.js and the browser\",\"icon\":{\"type\":\"icon\",\"url\":\"https://github.com/fluidicon.png\",\"aspectRatio\":0},\"thumbnail\":{\"type\":\"thumbnail\",\"url\":\"https://avatars2.githubusercontent.com/u/70011?s=400&v=4\",\"width\":400,\"height\":400,\"aspectRatio\":1}}" %}

{% embed data="{\"url\":\"https://randomapi.com/\",\"type\":\"link\",\"title\":\"RandomAPI :: Index\",\"description\":\"Easily generate fake data for populating your mockups and testing your applications.\",\"icon\":{\"type\":\"icon\",\"url\":\"https://randomapi.com/img/favicon.png\",\"aspectRatio\":0}}" %}

### 온라인 REST API 테스트 서비스 {#online-rest-api-test}

{% embed data="{\"url\":\"https://reqres.in/\",\"type\":\"link\",\"title\":\"Reqres - A hosted REST-API ready to respond to your AJAX requests\",\"description\":\"A hosted REST-API ready to respond to your AJAX requests\"}" %}

{% embed data="{\"url\":\"https://jsonplaceholder.typicode.com/\",\"type\":\"link\",\"title\":\"JSONPlaceholder - Fake online REST API for developers\",\"description\":\"Fake online REST API for developers\",\"icon\":{\"type\":\"icon\",\"url\":\"https://jsonplaceholder.typicode.com/favicon.ico\",\"aspectRatio\":0}}" %}

{% embed data="{\"url\":\"https://restcountries.eu/\",\"type\":\"link\",\"title\":\"REST Countries\",\"description\":\"Get information about countries via a RESTful API\",\"icon\":{\"type\":\"icon\",\"url\":\"https://restcountries.eu/img/favicon.ico\",\"aspectRatio\":0}}" %}

{% embed data="{\"url\":\"http://myjson.com/\",\"type\":\"link\",\"title\":\"Myjson - A simple json storage and hosting service\",\"icon\":{\"type\":\"icon\",\"url\":\"http://myjson.com/assets/favicon-5b1c39a7ac26f7c35be83b2b40e907c2.ico\",\"aspectRatio\":0},\"caption\":\"https://api.myjson.com/16oqx2\"}" %}

### 로컬 REST API 테스트 서버 {#local-rest-api-test}

JSON Server는 손쉽게 REST API를 구축해주는 라이브러리 입니다. REST API 서버의 기본적인 기능을 대부분 갖추고 있으며 테스트 용도로 사용됩니다.

{% embed data="{\"url\":\"https://github.com/typicode/json-server\",\"type\":\"link\",\"title\":\"typicode/json-server\",\"description\":\"json-server - Get a full fake REST API with zero coding in less than 30 seconds \(seriously\)\",\"icon\":{\"type\":\"icon\",\"url\":\"https://github.com/fluidicon.png\",\"aspectRatio\":0},\"thumbnail\":{\"type\":\"thumbnail\",\"url\":\"https://avatars0.githubusercontent.com/u/5502029?s=400&v=4\",\"width\":128,\"height\":128,\"aspectRatio\":1}}" %}

#### 설치 {#install}

NPM 인스톨\(install\) 명령을 사용해 `json-server` 모듈을 설치합니다.

```text
$ npm i -g json-server
```

#### 에셋 & db.json 준비 {#assets-db-json}

[에셋 자료](https://github.com/yamoo9/assets/tree/master/images/ediya)를 보관할 디렉토리 및 REST API 테스트 할 [db.json](https://gist.github.com/yamoo9/990c01dc4640b48e65ac62398a39dd80) 파일을 준비합니다.

```markup
<!-- 이미지 호스팅 경로 -->
https://raw.githubusercontent.com/yamoo9/assets/master/images/ediya/{{이미지-파일-경로}}
```

#### 테스트 서버 구동

JSON Server 명령을 사용해 테스트 서버를 구동합니다.

```bash
# json-server --watch db.json --port 포트번호
$ json-server -w db.json -p 4000
```

![&#xBE0C;&#xB77C;&#xC6B0;&#xC800;&#xC5D0;&#xC11C; &#xAD6C;&#xB3D9;&#xB41C; JSON Server](../.gitbook/assets/image%20%2816%29.png)

#### 홈페이지 \(Homepage\)

`./public`디렉토리 내부의 인덱스 파일을 보여줍니다.

```typescript
GET /
```

#### 데이터베이스 \(Database\)

db.json 파일의 데이터를 화면에 출력합니다.

```typescript
GET /db
```

#### 라우트 \(Routes\)

기본적으로 제공되는 라우트는 다음과 같습니다. [사용자 정의 라우팅 설정](https://github.com/typicode/json-server#add-custom-routes)도 가능합니다.

```typescript
GET    /posts
GET    /posts/:id
POST   /posts
PUT    /posts/:id
PATCH  /posts/:id
DELETE /posts/:id
```

#### 데이터 읽기/쓰기/수정/제거

[Postman](rest-api-test.md#postman)을 사용해 데이터를 읽고, 쓰고, 수정하거나, 제거할 수 있습니다. 즉, [CRUD](https://ko.wikipedia.org/wiki/CRUD) 를 수행할 수 있습니다.

{% hint style="info" %}
CRUD는 대부분의 컴퓨터 소프트웨어가 가지는 기본적인 데이터 처리 기능인 Create\(생성\), Read\(읽기\), Update\(갱신\), Delete\(삭제\)를 묶어서 일컫는 말입니다. 사용자 인터페이스가 갖추어야 할 기능\(정보의 참조/검색/갱신\)을 가리키는 용어로 사용되기도 합니다.
{% endhint %}

![JSON Server + Postman](../.gitbook/assets/image%20%2815%29.png)

#### 전체 텍스트 검색 \(Full-Text Search\)

쿼리\(`?q`\) 뒤에 키워드를 입력하면 검색 요청된 데이터만 읽어옵니다.

```text
GET /posts?q=internet
```

#### 필터 \(Filter\)

쿼리\(`?`\) 뒤에 `키1=값1&키2=값2` 형태로 입력하여 요청하면 데이터를 필터링 하여 읽어올 수 있습니다. 객체의 속성 값을 통해 필터링 하려면 포인트\(`.`\)를 사용합니다.

```typescript
GET /posts?title=ediyamenu&author=yamoo9
GET /posts?id=2&id=5
GET /comments?author.name=yamoo9
```

#### 페이지 설정 \(Paginate\)

페이지를 사용하려면 `_page`, `_limit`를 사용해 요청합니다. `first`, `prev`, `next`와 `last`링크를 제공합니다.

```typescript
GET /posts?_page=6 // 기본적으로 10개 항목이 반환
GET /posts?_page=9&_limit=15
```

#### 정렬 \(sort\) {#정렬-sort}

정렬을 수행할 때는 쿼리 파라미터\(query parameters\)로 `_sort` 와 `_order`를 설정합니다. 각 요청은 `id`를 기준으로 오름차순\(ASC\), 내림차순\(DESC\)으로 데이터를 정렬해 가져옵니다.

```typescript
GET /memo?_sort=id&_order=ASC // 기본 값: 오름차순(ASC)
GET /memo?_sort=id&_order=DESC
```

#### 자르기 \(Slice\)

`_start`, `_end`, `_limit` 설정을 사용해 요청하면 데이터 중 일부분만을 읽어 들입니다. [Array.slice](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/slice) 와 동일하게 작동합니다.

```typescript
GET /posts?_start=20&_end=30
GET /posts/1/comments?_start=20&_end=30
GET /posts/1/comments?_start=20&_limit=10
```

#### 연산자 \(Operators\) {#연산자-operators}

특정 필드가 주어진 값보다 크거나 작은 데이터들을 불러올 때 `_gte`, `_lte`, `_ne` 를 사용합니다.

| **약어** | **풀이** | **설명** |
| --- | --- | --- | --- |
| gte | Greater Then or Equal to | 크거나 같습니다. |
| lte | Less Then or Equal to | 작거나 같습니다. |
| ne | Not Equal | 같지 않습니다. |

```typescript
GET /posts?views_gte=10&views_lte=20
GET /memo?id_lte=7
GET /memo?id_ne=10
```

{% hint style="info" %}
여기에 소개되지 않은 json-server의 기능은 [공식 매뉴얼](https://github.com/typicode/json-server)을 참고하세요.
{% endhint %}

