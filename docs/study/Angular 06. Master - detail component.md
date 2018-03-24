# 5. Master / 세부사항 Component
현재 HeroesComponent에는 영웅의 목록과 선택한 영웅의 세부 정보가 모두 표시됩니다.

애플리케이션이 성장함에 따라 하나의 컴포넌트에 모든 기능을 유지하는 것은 유지 보수 할 수 없습니다. 큰 컴포넌트를 작은 하위 컴포넌트로 나눠서 각 컴포넌트는 특정 작업이나 워크 플로에 중점을 둡니다.

이 페이지에서 영웅의 세부 정보를 별도의 재사용 가능한 HeroDetailsComponent로 이동하여 첫 번째 단계를 수행하게됩니다.

HeroesComponent는 영웅의 목록 만 표시합니다. HeroDetailsComponent는 선택된 영웅의 세부 사항을 보여줍니다.



## HeroDetailComponent 만들기
----------

Angular CLI를 사용하여 hero-detail이라는 새 컴포넌트를 생성합니다.


![](https://d2mxuefqeaa7sj.cloudfront.net/s_69A6737C61236F505489F346AD6588E2FA7947E90A31B8EF96FFC1499F2620F7_1520950568300_image.png)




## 템플릿 작성

HeroesComponent 템플릿의 맨 아래에서 영웅 상세에 대한 HTML을 잘라내 HeroDetailComponent 템플릿의 생성 된 상용구 위에 붙여 넣습니다.

붙여 넣은 HTML은 selectedHero를 참조합니다. 새로운 HeroDetailComponent는 선택된 영웅뿐만 아니라 모든 영웅을 나타낼 수 있습니다. 따라서 템플릿의 "히어로"를 "selectedHero"로 바꾸십시오.

완료되면 HeroDetailComponent 템플릿은 다음과 같이 표시됩니다.

src/app/hero-detail/hero-detail.component.html

    <div *ngIf="hero">
    
      <h2>{{ hero.name | uppercase }} Details</h2>
      <div><span>id: </span>{{hero.id}}</div>
      <div>
        <label>name:
          <input [(ngModel)]="hero.name" placeholder="name"/>
        </label>
      </div>
    
    </div>


## @Input () hero 속성을 추가하십시오.

HeroDetailComponent 템플릿은 Hero 유형의 컴포넌트의 영웅 속성에 바인딩됩니다.

HeroDetailComponent 클래스 파일을 열고 영웅 심볼을 가져옵니다.

src/app/hero-detail/hero-detail.component.ts (import Hero)

    import { Hero } from '../hero';

영웅 속성은 @Input () 데코레이터로 주석된 Input 속성이어야합니다. 외부 HeroesComponent가 이와 같이 바인딩하기 때문입니다.


    <app-hero-detail [hero]="selectedHero"></app-hero-detail>

src/app/hero-detail/hero-detail.component.ts (import Input)

    import { Component, OnInit, Input } from '@angular/core';

Add a `hero` property, preceded by the `@``[Input](https://angular.io/api/core/Input)``()` decorator.


    @Input() hero: Hero;

HeroDetailComponent 클래스에 대해 변경해야 할 유일한 변경 사항입니다. 더 이상 속성이 없습니다.  이 컴포넌트는 단순히 영웅 속성을 통해 영웅 개체를 수신하고 표시합니다.




## HeroDetailComponent 표시
----------

HeroesComponent는 여전히 마스터 / 세부 정보보기입니다.

템플리트의 해당 부분을 자르기 전에 영웅 세부 사항을 자체적으로 표시했습니다. 이제 HeroDetailComponent에 위임 할 것입니다.

두 구성 요소에는 상위 / 하위 관계가 있습니다. 부모 HeroesComponent는 사용자가 목록에서 영웅을 선택할 때마다 새로운 영웅을 보내서 HeroDetailComponent 하위를 제어합니다.

HeroesComponent 클래스는 변경하지 않지만 템플릿을 변경합니다.



## HeroDetailComponent 업데이트
----------

HeroDetailComponent 선택자는 'app-hero-detail'입니다. HeroesComponent 템플릿 맨 아래에 <app-hero-detail> 요소를 추가합니다.이 요소는 영웅 상세보기가 있어야합니다.

HeroesComponent.selectedHero를 다음과 같이 요소의 hero 속성에 바인딩합니다.

heroes.component.html (HeroDetail binding)

    <app-hero-detail [hero]="selectedHero"></app-hero-detail>

[hero] = "selectedHero"는 앵귤러의 속성 바인딩입니다.

HeroesComponent의 selectedHero 속성에서 HeroDetailComponent의 hero 속성에 매핑되는 대상 요소의 hero 속성에 대한 단방향 데이터 바인딩입니다.

이제 사용자가 목록에서 영웅을 클릭하면 선택한 영웅이 변경됩니다. selectedHero가 변경되면 속성 바인딩이 영웅을 업데이트하고 HeroDetailComponent가 새 영웅을 표시합니다.

수정된 HeroesComponent 템플릿은 다음과 같아야합니다.

heroes.component.html

    <h2>My Heroes</h2>
    
    <ul class="heroes">
      <li *ngFor="let hero of heroes"
        [class.selected]="hero === selectedHero"
        (click)="onSelect(hero)">
        <span class="badge">{{hero.id}}</span> {{hero.name}}
      </li>
    </ul>
    
    <app-hero-detail [hero]="selectedHero"></app-hero-detail>

무엇이 바뀌 었습니까?
이전과 마찬가지로 사용자가 영웅 이름을 클릭 할 때마다 영웅 세부 사항이 영웅 목록 아래에 표시됩니다. 이제 HeroDetailComponent가 HeroesComponent 대신 세부 정보를 제공합니다.

원래 HeroesComponent를 두 가지 구성 요소로 리팩토링하면 현재와 미래 모두 혜택을 얻을 수 있습니다.


1. 책임을 줄임으로써 HeroesComponent를 간소화했습니다.
2. 상위 HeroesComponent를 건드리지 않고 HeroDetailComponent를 풍부한 영웅 편집기로 발전시킬 수 있습니다.
3. 히어로 자세히보기를 터치하지 않고 HeroesComponent를 진화시킬 수 있습니다.
4. HeroDetailComponent는 향후 구성 요소의 템플리트에서 다시 사용할 수 있습니다.

