# 라우팅

### 라우팅을 사용하는 이유 {#why}

`*NgIf` 디렉티브 또는 `[hidden]` 속성 바인딩을 통해 페이지에 컴포넌트를 숨기거나 표시할 수 있습니다. 이를 활용해  마치 페이지가 변경된 것처럼 UI를 구현할 수 있지만, 브라우저 주소 영역의 URL이 바뀌지는 않습니다. 뿐만 아니라 다음과 같은 문제점이 발생합니다.

1. 페이지를 새로고침 하면 애플리케이션이 초기화 됩니다. 즉, 검색된 페이지를 새로고침 하면 결과가 사라집니다.
2. 애플리케이션의 현재 페이지를 북마크\(즐겨찾기\)에 저장할 수 없어 현재 페이지 링크를 제공할 수 없습니다.

이 문제를 해결하기 위해서는 브라우저 주소 영역의 URL을 통해 애플리케이션의 현재 상태\(State\)를 기억하고 찾아갈 수 있도록 만들어야 합니다. 네. 맞습니다. 그것이 라우팅이 필요한 이유입니다.

{% hint style="info" %}
IT, 컴퓨터 과학 분야에서 [상태\(State\)](https://en.wikipedia.org/wiki/State_%28computer_science%29) 란? 애플리케이션과 사용자 간의 인터랙션\(상호작용\)에 따라 기억된  정보를 말합니다. 다시 말해 애플리케이션에 접근할 수 있는 저장된 정보\(변수\)의 현재 값입니다.

브라우저 주소 영역 URL에 많은 정보를 저장할 수는 없지만, 애플리케이션 페이지의 상태 정보를 저장해 URL에 따라 페이지의 상태\(데이터\)를 불러와 사용자에게 변경된 페이지를 보여줄 수 있습니다.
{% endhint %}

애플리케이션 URL에 상태를 저장할 수 있으므로 특정 URL에 따라 설정된 페이지를 사용자에게 보여줄 수 있습니다. 

### 서버 사이드 라우팅 {#server-side-routing}

서버 사이드 라우팅으로 구축된 기존의 애플리케이션은 사용자가 링크를 통해 브라우저 URL을 변경할 때 마다, URL에 따라 저장된 상태를 통해 만들어진 HTML 페이지를 전달 받도록 서버에 요청합니다. 요청된 사항을 서버에서 반영해 새로운 페이지를 만들어 사용자에게 전달해야 하기 때문에 변경된 페이지를 사용자에게 표시하는데 다소 시간이 소요됩니다.

![&#xC11C;&#xBC84; &#xCE21;&#xC5D0;&#xC11C; &#xC81C;&#xACF5;&#xD558;&#xB294; &#xB77C;&#xC6B0;&#xD305;](../.gitbook/assets/image%20%2818%29.png)

### 클라이언트 사이드 라우팅 {#client-side-routing}

반면 클라이언트 사이드 라우팅이 반영된 애플리케이션은 변경사항을 처리하기 위해 URL이 변경 되어도 서버에 요청하지 않습니다. 즉, 애플리케이션 내부적으로 페이지를 변경합니다. 서버에서 페이지를 만들어 전달 하고, 그것을 브라우저에서 받아 사용자에게 표시하는 것이 아니어서 변경된 페이지를 표시하는 속도가 상당히 빠릅니다.

물론 애플리케이션 첫 페이지는 URL을 통해 서버에 해당 페이지를 렌더링 하는데 필요한 HTML, CSS, JavaScript, 이미지 파일 등을 요청해야 합니다. 하지만 이후 URL 변경에 따른 변동 내용은 모두 클라이언트 애플리케이션에서 처리합니다. 서버에서 응답 받은 페이지는 단 하나 뿐이라, 이를 [싱글 페이지 애플리케이션\(SPA\)](https://ko.wikipedia.org/wiki/%EC%8B%B1%EA%B8%80_%ED%8E%98%EC%9D%B4%EC%A7%80_%EC%95%A0%ED%94%8C%EB%A6%AC%EC%BC%80%EC%9D%B4%EC%85%98)라고 부릅니다.

![](../.gitbook/assets/image%20%2822%29.png)

### SPA의 장점 {#spa-benefit}

싱글 페이지 애플리케이션의 장점으로 거론되는 것들은 다음과 같습니다.

1. URL이 바뀔 때마다 서버 요청을 통해 새로운 페이지를 렌더링 하는 것보다 페이지 렌더링 속도가 훨씬 빠릅니다.
2. 보다 작은 대역폭\([bandwidth](https://ko.wikipedia.org/wiki/%EB%8C%80%EC%97%AD%ED%8F%AD_%28%EC%BB%B4%ED%93%A8%ED%8C%85%29)\)이 필요합니다. URL이 변경될 때마다 페이지의 일부만 변경하는 API를 사용합니다.
3. 프론트 엔드, 백엔드 개발자를 구분하지 않고도 프론트 엔드 개발자가 서비스의 대부분 기능을 구축할 수 있습니다.

### SPA의 단점 {#spa-weakness}

싱글 페이지 애플리케이션이 장점만 있지는 않습니다. 단점을 나열하면 다음과 같습니다. [사실 단점 이라기 보다는 SPA 구조 상 당연히 발생할 수 밖에 없는 상황으로 이해되어야 합니다.](http://m.mkexdev.net/374) 즉, 모든 애플리케이션에 SPA가 적합한 것은 아니기에 프로젝트 기획 과정에서 SPA 반영을 고민할 필요가 있습니다.

1. 초기 구동 속도가 느립니다. 하지만 리소스를 청크\(Chunk\) 단위로 묶어 부분 다운로드 방식으로 대응할 수 있습니다.
2. [검색엔진최적화\(SEO\)](https://ko.wikipedia.org/wiki/%EA%B2%80%EC%83%89_%EC%97%94%EC%A7%84_%EC%B5%9C%EC%A0%81%ED%99%94) 문제가 있습니다. 이 문제는 [SPA를 SSL 방식으로 변경해 서비스하면 해결](https://universal.angular.io/)할 수 있습니다.
3. 모든 핵심 로직이 JavaScript로 구현되어 클라이언트에서 서비스 되므로 보안에 취약한 문제가 있습니다.
4. 오래된 브라우저\(IE 8 이하\)를 지원하지 않습니다. 즉, 구형 브라우저를 지원하는 프로젝트에 적합하지 않습니다.

### Angular로 구성하는 SPA

Angular는 SPA를 구현할 수 있는 몇 가지 모듈을 제공합니다. Angular에서 제공하는 컴포넌트 라우터를 사용해 SPA를 구성하는 방법을 학습해보겠습니다. 이 섹션에서 배우는 내용은 다음과 같습니다.

* 애플리케이션의 URL에 따라 화면에 보여질 컴포넌트를 구성하는 방법
* 서버 요청 없이 브라우저 URL을 탐색해 클라이언트 측에서 처리하는 방법
* 매개 변수 또는 쿼리가 설정된 URL을 통해 페이지를 처리하는 방법 
* 중첩된 URL을 통해 페이지를 제공하는 방법
* 라우터 가드를 사용해 접근이 제한되는 페이지를 구성하는 방법

### 

