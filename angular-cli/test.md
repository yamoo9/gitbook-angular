# 테스트

Angular는 테스트를 손쉽게 수행할 수 있는 기능이 포함되어 있습니다. Angular 테스트의 기본 메커니즘은 [Karma](https://karma-runner.github.io/) + [`Jasmine`](https://jasmine.github.io/) 입니다. `ng generate` 명령을 통해 Angular 파일을 생성할 때마다 테스트 파일\(`.spec.ts`\) 또한 자동으로 추가됩니다.

{% hint style="info" %}
이러한 유형의 테스트를 유닛 테스트\(Unit Test\)라고 합니다. 테스트를 작성하여 코드 단위 하나만 테스트하고, 각 테스트 사례는 다른 테스트 사례와 독립적으로 수행되기 때문입니다.
{% endhint %}

단 한 줄의 명령어로 모든 유닛 테스틀 수행할 수 있습니다.

```bash
$ ng test
```

명령을 수행하면 프로젝트가 빌드된 이후, 모든 테스트가 실행되고, 오류가 발생하면 터미널에 출력됩니다. 테스트가 실행되면 브라우저가 열립니다. 테스트를 지속적으로 처리 하려면 브라우저 창을 닫지 말아야 합니다.

![](../.gitbook/assets/image%20%2821%29.png)

