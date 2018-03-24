# 6. 서비스
Tour of Heroes HeroesComponent는 현재 가짜 데이터를 받고 표시하고 있습니다.

이 튜토리얼의 리팩터링 후 HeroesComponent는 기울이고 뷰 지원에 초점을 맞 춥니 다. 또한 모의 서비스로 단위 테스트를하는 것이 더 쉬울 것입니다.

서비스가 필요한 이유
구성 요소는 데이터를 직접 가져 오거나 저장하면 안되며 고의적으로 가짜 데이터를 표시해서는 안됩니다. 그들은 데이터를 표현하고 데이터 액세스를 서비스에 위임하는 데 집중해야합니다.

이 자습서에서는 모든 응용 프로그램 클래스가 영웅을 얻는 데 사용할 수있는 HeroService를 만듭니다. 새로운 서비스를 만드는 대신 Angular dependency injection을 사용하여 HeroesComponent 생성자에 주입합니다.

서비스는 서로를 모르는 클래스간에 정보를 공유하는 좋은 방법입니다. MessageService를 만들고 두 곳에서 주입합니다.

HeroService에서 서비스를 사용하여 메시지를 보냅니다.
해당 메시지를 표시하는 MessagesComponent.




## 히어로 서비스 생성
----------

src/app/hero.service.ts (new service)

    content_copyimport { Injectable } from '@angular/core';
    
    @Injectable()
    export class HeroService {
    
      constructor() { }
    
    }


**@ injectable 서비스**
새로운 서비스는 Angular Injectable 심볼을 가져오고 클래스를 @Injectable () 데코레이터로 주석 처리합니다.

@Injectable () 데코레이터는 Angular에게이 서비스 자체가 의존성을 주입했음을 알립니다. 그것은 지금은 의존성이 없지만 곧있을 것입니다. 그것이하든 그렇지 않든, 데코레이터를 지키는 것이 좋습니다.

앵귤러 스타일 가이드 라인은 그것을 지킬 것을 강력하게 권고하고 linter는이 규칙을 집행합니다.


**히어로 데이터 가져오기**
HeroService는 웹 서비스, 로컬 스토리지 또는 모의 데이터 소스 등 어디에서나 영웅 데이터를 얻을 수 있습니다.

구성 요소에서 데이터 액세스를 제거하면 컴포넌트를 건드리지 않고도 언제든지 구현에 대한 생각을 바꿀 수 있습니다. 그들은 서비스가 어떻게 작동 하는지를 모릅니다.

이 자습서의 구현은 계속 모의 영웅을 제공 할 것입니다.

영웅과 영웅을 가져 오십시오.


    import { Hero } from './hero';
    import { HEROES } from './mock-heroes';

Add a `getHeroes` method to return the *mock heroes*.


    getHeroes(): Hero[] {
      return HEROES;
    }



## HeroService 제공
----------

Dependency Injection System에서 HeroService를 제공해야 Angular가 HeroesComponent에 HeroService를 주입 할 수 있습니다.

HeroService를 제공하는 방법에는 HeroesComponent, AppComponent, AppModule 등 여러 가지가 있습니다. 각 옵션에는 장단점이 있습니다.

이 자습서는 AppModule에서 제공하도록 선택합니다.

이것은 --module = app을 추가하여 CLI에 자동으로 제공하도록 CLI에 요청했을 수있는 인기있는 선택입니다.


![](https://d2mxuefqeaa7sj.cloudfront.net/s_506F10771B572B3A99B887CFBD3C379E8AB9DA048FC96704473FFE683803FF35_1520951588396_image.png)


AppModule 클래스를 열고 HeroService를 가져 와서 @ NgModule.providers 배열에 추가합니다.

src/app/app.module.ts (providers)

    providers: [
        HeroService,
    /* . . . */
      ],

providers 배열은 HeroService의 단일 공유 인스턴스를 만들고이를 요청하는 클래스에 삽입하도록 Angular에 지시합니다.

이제 HeroService를 HeroesComponent에 연결할 준비가되었습니다.

이것은 HeroService를 제공하고 사용할 수있는 임시 코드 샘플입니다. 이 시점에서 코드는 HeroService와 "최종 코드 검토"에서 다를 것입니다.

공급자에 대한 자세한 내용은 공급자 안내서를 참조하십시오.



## HeroesComponent 업데이트

HeroesComponent 클래스 파일을 엽니 다.

HEROES 가져오기는 더 이상 필요하지 않으므로 삭제하십시오. 대신 HeroService를 가져 오십시오.

src/app/heroes/heroes.component.ts (import HeroService)

    import { HeroService } from '../hero.service';

Replace the definition of the `heroes` property with a simple declaration.

    heroes: Hero[];


## Hero Service 주입
----------
    constructor(private heroService: HeroService) { }

매개 변수는 동시에 개인 heroService 속성을 정의하고이를 HeroService 주입 사이트로 식별합니다.

Angular가 HeroesComponent를 만들면 Dependency Injection 시스템은 heroService 매개 변수를 HeroService의 singleton 인스턴스로 설정합니다.



## getHeroes 추가
----------
    getHeroes(): void {
      this.heroes = this.heroService.getHeroes();
    }



## ngOnInit에서 호출
----------

생성자에서 getHeroes ()를 호출 할 수는 있지만 가장 좋은 방법은 아닙니다.

속성에 와이어 링 생성자 매개 변수와 같은 간단한 초기화를 위해 생성자를 예약하십시오. 생성자는 아무 것도해서는 안됩니다. 실제 데이터 서비스처럼 원격 서버에 HTTP 요청을하는 함수를 호출해서는 안됩니다.

대신 ngOnInit 라이프 사이클 후크 내에서 getHeroes ()를 호출하고 HeroesComponent 인스턴스를 생성 한 후 적절한 시점에 Angular call ngOnInit을 호출합니다.



    ngOnInit() {
      this.getHeroes();
    }




## Observable 데이터
----------

HeroService.getHeroes () 메서드에는 HeroService가 영웅을 동 기적으로 가져올 수 있음을 의미하는 동기식 서명이 있습니다. HeroesComponent는 영웅을 동기적으로 가져올 수 있는 것처럼 getHeroes() 결과를 사용합니다.


    this.heroes = this.heroService.getHeroes();

이 기능은 실제 앱에서는 작동하지 않습니다. 현재 서비스가 모의 영웅을 반환하기 때문에 지금은 벗어나고 있습니다. 그러나 곧 응용 프로그램은 원격 서버에서 영웅을 가져옵니다. 이는 원래 비동기 작업입니다.

HeroService는 서버가 응답하기를 기다려야하며 getHeroes ()는 영웅 데이터로 즉시 반환 할 수 없으며 서비스가 대기하는 동안 브라우저가 차단되지 않습니다.

HeroService.getHeroes ()에는 어떤 종류의 비동기 서명이 있어야합니다.

그것은 콜백을 걸릴 수 있습니다. 그것은 약속을 반환 할 수 있습니다. Observable을 반환 할 수 있습니다.

이 자습서에서 HeroService.getHeroes ()는 Observable을 부분적으로 반환합니다. Angular HttpClient.get 메서드를 사용하여 영웅을 가져오고 HttpClient.get ()이 Observable을 반환하기 때문입니다.



## Observable 히어로 서비스
----------

Observable은 RxJS 라이브러리의 핵심 클래스 중 하나입니다.

나중에 HTTP 튜토리얼에서 Angular의 HttpClient 메소드가 RxJS Observables를 리턴한다는 것을 알게 될 것이다. 이 자습서에서는 RxJS of () 함수를 사용하여 서버에서 데이터를 가져 오는 과정을 시뮬레이션합니다.

HeroService 파일을 열고 RxJS에서 Observable 및 Symbol을 가져옵니다.

src/app/hero.service.ts (Observable imports)

    import { Observable } from 'rxjs/Observable';
    import { of } from 'rxjs/observable/of';

Replace the `getHeroes` method with this one.

    getHeroes(): Observable<Hero[]> {
      return of(HEROES);
    }

of (HEROES)는 모의 영웅의 배열 인 Observable <Hero>를 반환합니다.

HTTP 튜토리얼에서는 HttpClient.get <Hero []> ()를 호출하여 HTTP 응답의 본문에서 영웅 배열 인 Observable <Hero []>를 반환합니다.




## HeroesComponent를 구독
----------

HeroService.getHeroes 메서드는 Hero []를 반환하는 데 사용됩니다. Observable <Hero []>를 반환합니다.

HeroesComponent의 차이점을 조정해야합니다.

getHeroes 메소드를 찾아 다음 코드로 대체하십시오 (비교를 위해 이전 버전과 나란히 표시).

Observable

    getHeroes(): void {
      this.heroService.getHeroes()
          .subscribe(heroes => this.heroes = heroes);
    }

Original

    getHeroes(): void {
      this.heroes = this.heroService.getHeroes();
    }


Observable.subscribe ()가 중요한 차이입니다.

이전 버전에서는 영웅의 배열을 구성 요소의 heroes 속성에 할당합니다. 서버가 영웅을 즉시 반환 할 수 있거나 서버의 응답을 기다리는 동안 브라우저가 UI를 고정시킬 수있는 것처럼 할당은 동 기적으로 발생합니다.

HeroService가 실제로 원격 서버를 요청할 때 작동하지 않습니다.

새로운 버전은 Observable이 영웅들의 배열을 방출 할 때까지 기다립니다. 지금부터 또는 몇 분 후에 일어날 수 있습니다. 그런 다음 subscribe는 생성 된 배열을 콜백에 전달합니다. 콜백은 구성 요소의 heroes 속성을 설정합니다.

이 비동기 방식은 HeroService가 서버에서 영웅을 요청할 때 작동합니다.





## 메시지 서비스 생성
----------

이 섹션에서는 

1. 화면 맨 아래에 앱 메시지를 표시하는 MessagesComponent를 추가하십시오.
2. 표시 할 메시지를 보낼 수있는 주류의 앱용 MessageService를 작성하십시오.
3. HeroService에 MessageService를 주입합니다.
4. HeroService가 영웅을 성공적으로 가져올 때 메시지를 표시합니다.

**Create** ***MessagesComponent***


![](https://d2mxuefqeaa7sj.cloudfront.net/s_506F10771B572B3A99B887CFBD3C379E8AB9DA048FC96704473FFE683803FF35_1520952140242_image.png)


/src/app/app.component.html

    <h1>{{title}}</h1>
    <app-heroes></app-heroes>
    <app-messages></app-messages>


**Create the** ***MessageService***

![](https://d2mxuefqeaa7sj.cloudfront.net/s_506F10771B572B3A99B887CFBD3C379E8AB9DA048FC96704473FFE683803FF35_1520952160595_image.png)


/src/app/message.service.ts

    import { Injectable } from '@angular/core';
    
    @Injectable()
    export class MessageService {
      messages: string[] = [];
    
      add(message: string) {
        this.messages.push(message);
      }
    
      clear() {
        this.messages = [];
      }
    }

이 서비스는 메시지 캐시와 두 가지 방법, 즉 캐시에 메시지를 추가 ()하고 캐시를 clear ()하는 방법을 제공합니다.




## **Inject it into the 히어로 서비스**
----------

/src/app/hero.service.ts (import MessageService)

    import { MessageService } from './message.service';

private messageService 속성을 선언하는 매개 변수로 생성자를 수정합니다. Angular는 HeroService를 만들 때 해당 속성에 싱글톤 MessageService를 주입합니다.


    constructor(private messageService: MessageService) { }


**이것은 전형적인 "서비스 안에 서비스"시나리오입니다 HeroesComponent에 주입 된 HeroService에 MessageService를 주입합니다.**



## Send a message from `HeroService`
----------
    getHeroes(): Observable<Hero[]> {
      // Todo: send the message _after_ fetching the heroes
      this.messageService.add('HeroService: fetched heroes');
      return of(HEROES);
    }



## HeroService의 메시지 표시
----------

MessagesComponent는 영웅을 가져올 때 HeroService가 보낸 메시지를 포함하여 모든 메시지를 표시해야합니다.

MessagesComponent를 열고 MessageService를 가져 오십시오.

/src/app/messages/messages.component.ts (import MessageService)

    import { MessageService } from '../message.service';

public messageService 속성을 선언하는 매개 변수로 생성자를 수정합니다. Angular는 HeroService를 만들 때 해당 속성에 싱글 톤 MessageService를 주입합니다.


    constructor(public messageService: MessageService) {}


messageService 속성은 템플릿에서 바인딩하려고하기 때문에 public이어야합니다.

앵귤러는 퍼블릭 컴포넌트 속성에만 바인딩됩니다.




## MessageService에 바인딩
----------

CLI에서 생성 한 MessagesComponent 템플리트를 다음으로 대체하십시오.

src/app/messages/messages.component.html

    <div *ngIf="messageService.messages.length">
    
      <h2>Messages</h2>
      <button class="clear"
              (click)="messageService.clear()">clear</button>
      <div *ngFor='let message of messageService.messages'> {{message}} </div>
    
    </div>

이 템플릿은 구성 요소의 messageService에 직접 바인딩됩니다.


- ngIf는 표시 할 메시지가있는 경우에만 메시지 영역을 표시합니다.
- ngFor는 반복되는 <div>요소의 메시지 목록을 표시합니다.
- Angular 이벤트 바인딩은 버튼의 클릭 이벤트를 MessageService.clear ()에 바인딩합니다.

아래의 "최종 코드 검토"탭 중 하나에 나열된대로 messages.component.css에 개인 CSS 스타일을 추가하면 메시지가 더 잘 보입니다.
브라우저가 새로 고침되고 페이지에 영웅 목록이 표시됩니다. 아래쪽으로 스크롤하면 메시지 영역의 HeroService에서 메시지를 볼 수 있습니다. "지우기"버튼을 클릭하면 메시지 영역이 사라집니다.

