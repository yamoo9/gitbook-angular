# \[ngSwitch\] 디렉티브

`[ngSwitch]`는 속성 디렉티브로 `*ngSwitchCase`, `*ngSwitchDefault` 구조 디렉티브와 다음에 유의해야 합니다. 이전 예제인 `*ngIf` 구조 디렉티브 예제를 `[ngSwitch]`, `*ngSwitchCase`, `*ngSwitchDefault`를 사용한 예제로 바꿔 봅시다.

```markup
...

<p [ngSwitch]="is_renderting">
  <ng-template *ngSwitchCase="true">is_renderting 값이 참이면 화면에 렌더링 됩니다.</ng-template>
  <ng-template *ngSwitchDefault>is_renderting 디렉티브 값이 거짓이면 화면에 렌더링 됩니다.</ng-template>
</p>
```

`*ngSwitchCase` 디렉티브는 조건이 늘어날 때마다 사용이 가능합니다. Switch - case 문을 떠올리면 쉽게 이해할 수 있을 겁니다. 상대적으로 혼동스러웠던 `*ngIf` 보다는 친숙한 편입니다. 위 코드는 다음과 같이 변경 사용이 가능합니다. `<ng-container>` 요소는 `<ng-template>` 요소와 마찬가지로 화면에 렌더링 되지 않으며, 그룹 생성을 목적으로 사용합니다.

```markup
<ng-container [ngSwitch]="is_renderting">
  <p *ngSwitchCase="true">is_renderting 값이 참이면 화면에 렌더링 됩니다.</p>
  <p *ngSwitchCase="false">is_renderting 값이 거짓이면 화면에 렌더링 됩니다.</p>
</ng-container>
```

