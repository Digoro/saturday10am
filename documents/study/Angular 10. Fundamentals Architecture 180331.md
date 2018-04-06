# Fundamentals_Architecture_18/03/31

[ ] 모듈
[ ] 컴포넌트
[ ] 지시자
[ ] 서비스



# Angular Architecture 👮‍♂️ 
----------

Angular는 TypeScript로 웹 어플리케이션을 작성할 수 있는 플랫폼이자 프레임 워크입니다.

Angular 어플리케이션의 가장 기본적인 구성 요소(Building Block)는 NgModules입니다. 즉 Angular 어플리케이션은 NgModule들의 집합이라고 할 수 있습니다.


## Root Module

앵귤러 어플리케이션은 최소 한 개 이상의 모듈(루트 모듈)이 있어야 동작할 수 있습니다.


- 루트 모듈의 @ngModule 데코레이터 안에는 어플리케이션 전체의 설정 정보(declarations, imports, providers, bootstrap)가 들어갑니다. 
- 루트 모듈은 또한 **루트 컴포넌트**(/src/app/app.component.ts)를 부트스트랩 합니다.


    // imports
    import { BrowserModule } from '@angular/platform-browser';
    import { NgModule } from '@angular/core';
    import { FormsModule } from '@angular/forms';
    import { HttpModule } from '@angular/http';
    
    import { AppComponent } from './app.component';
    import { ItemDirective } from './item.directive';
    
    
    // @NgModule decorator with its metadata
    @NgModule({
      declarations: [
        AppComponent,
        ItemDirective
      ],
      imports: [
        BrowserModule,
        FormsModule,
        HttpModule
      ],
      providers: [],
      bootstrap: [AppComponent]
    })
    export class AppModule { }



## Root Component

앵귤러 어플리케이션에는 모든 컴포넌트의 부모 역할을 하는 루트 컴포넌트(/src/app/app.component.ts)가 있습니다.

![app.component.ts](https://d2mxuefqeaa7sj.cloudfront.net/s_969374E9BAEFEA4D82372A0CBE238ECBB4F656CC8FEBECF933D2B171094D257E_1522132220534_image.png)
![index.html](https://d2mxuefqeaa7sj.cloudfront.net/s_969374E9BAEFEA4D82372A0CBE238ECBB4F656CC8FEBECF933D2B171094D257E_1522132254358_image.png)


루트 템플릿이라고 할 수 있는 index.html 파일에 <app-root>를 이용해 루트 컴포넌트의 컴포넌트와 템플릿을 띄워주게 됩니다.



## Angular의 핵심 구성 요소
1. 모듈
2. 컴포넌트
3. 서비스 & DI
4. 라우터



## Angular Architecture 정리
1. Angular는 컴포넌트를 중심으로 Angular 구성요소를 조합하여 애플리케이션을 구축합니다. 
2. 뷰를 담당하는 컴포넌트를 중심으로 화면을 구성합니다.
3. 디렉티브와 서비스를 사용하여 애플리케이션 전역 관심사를 분리할 수 있습니다. 또한 컴포넌트는 필요 시 디렉티브와 서비스를 가져와 사용합니다. 
4. 라우터(Router)는 컴포넌트를 교체하는 방식으로 뷰를 전환하여 화면 간 이동을 구현합니다. 
5. 모듈은 관련된 구성 요소를 하나로 묶어 애플리케이션을 구성하는 하나의 단위를 만드는 역할을 합니다.







# 모듈 🕵️ 
----------

앵귤러에서 의미하는 모듈이란 **기능적**으로 관련된 구성요소(컴포넌트, 디렉티브, 파이프, 서비스)들을 하나의 단위로 묶는 메커니즘을 의미합니다. 


- 모듈은 관련이 있는 기능들이 모인 기능 단위로 애플리케이션을 구성하는 하나의 단위를 만듭니다. 
- 모듈은 다른 모듈과 결합할 수 있으며 Angular는 여러 모듈들을 조합하여 어플리케이션을 구성합니다.
- 컴포넌트, 지시자, 파이프, 서비스 등의 Angular 구성요소는 모듈에 등록되어야 사용할 수 있습니다.



## ECMAscript6 VS NgModule
| **ECMAScript6의 모듈**       | 애플리케이션을 구성하는 개별적 요소를 말한다. 일반적으로 모듈은 파일 단위로 분리되어 있으며 필요에 따라 애플리케이션은 명시적으로 모듈을 로드한다. 모듈은 애플리케이션에 분리되어 개별적으로 존재하다가 애플리케이션의 로드에 의해 비로소 애플리케이션의 일원이 된다. 모듈은 기능별로 분리되어 작성되므로 개발효율성과 유지보수성의 향상을 기대할 수 있다. |
| ------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Angular의 모듈(NgModule)** | 관련된 Angular 구성 요소를 하나로 묶어 애플리케이션을 구성하는 하나의 단위로 만드는 역할을 한다. 컴포넌트, 디렉티브, 서비스 등의 Angular 구성요소는 모듈에 등록되어야 사용할 수 있다.                                                                                    |




## NgModule metadata
- declaration : 컴포넌트, 파이프, 디렉티브 등을 명시해준다.
- imports : 다른 모듈을 가져오고 싶을 때 명시해준다.
- providers : 서비스를 providers에 명시해놓으면 제작한 앱의 모든 요소들에 서비스가 access 할 수 있습니다.
- bootstrap :  어플리케이션의 메인 뷰(진입점), 즉 다른 컴포넌트 뷰들을 모두 포함하는 루트 컴포넌트를 bootstrap에 명시해줍니다.



## 모듈 계층 구조
![Module A & Module B](https://d2mxuefqeaa7sj.cloudfront.net/s_969374E9BAEFEA4D82372A0CBE238ECBB4F656CC8FEBECF933D2B171094D257E_1522212657204_image.png)


컴포넌트와 템플릿은 함께 뷰를 만들고 템플릿 안에는 또 다른 컴포넌트가 포함될 수 있습니다. 그러므로 뷰는 계층 구조를 가질 수 있게 되고 아래의 그림과 같이 다른 NgModule에 속한 컴포넌트와 혼합되어 사용할 수 있습니다.


![Embedded Module](https://d2mxuefqeaa7sj.cloudfront.net/s_969374E9BAEFEA4D82372A0CBE238ECBB4F656CC8FEBECF933D2B171094D257E_1522212671411_image.png)







# 컴포넌트 👩‍🚀 
----------
## 컴포넌트 소개

컴포넌트는 Angular의 핵심 구성 요소로서 Angular 어플리케이션은 컴포넌트를 중심(CBD, Component Based Development)으로 구성됩니다. 컴포넌트의 역할은 어플리케이션의 화면을 구성하는 **뷰(View)**를 생성하고 관리하는 것입니다.



## @Component 데코레이터
- selector
- templateUrl
- styleUrls
![](https://d2mxuefqeaa7sj.cloudfront.net/s_969374E9BAEFEA4D82372A0CBE238ECBB4F656CC8FEBECF933D2B171094D257E_1522213534486_image.png)



- **클래스 데코레이터 :** @Component, @NgModule
- **프로퍼티 데코레이터 :** @Input, @Output
- **메소드 데코레이터 :** @HostListener
- **파라미터 데코레이터 :** @Inject



## 컴포넌트 동작 원리
![](https://d2mxuefqeaa7sj.cloudfront.net/s_969374E9BAEFEA4D82372A0CBE238ECBB4F656CC8FEBECF933D2B171094D257E_1522213628409_image.png)







# 서비스 & DI 👨‍🌾 
----------
## 서비스

서비스는 컴포넌트의 관심사와 **애플리케이션 전역 관심사를 분리**하기 위해 사용합니다. 컴포넌트와 서비스를 분리하여 작성하게 되면 컴포넌트는 복잡도가 낮아지고 서비스는 재사용할 수 있어 일관된 어플리케이션 개발이 가능하게 됩니다.



**@Injectable 데코레이터**

- @Injectable 데코레이터는 자신의 아래에 정의된 클래스가 주입 가능한(Injectable) 클래스임을 나타냅니다.
![Service](https://d2mxuefqeaa7sj.cloudfront.net/s_969374E9BAEFEA4D82372A0CBE238ECBB4F656CC8FEBECF933D2B171094D257E_1522218041098_image.png)






## 의존성 주입(Dependency Injection)

의존성 주입은 구성 요소 간의 의존 관계를 코드 내부가 아닌 외부의 설정파일 등을 통해 정의하는 디자인 패턴 중의 하나로서 구성 요소 간 결합도를 낮추고 재사용성을 높인다.


의존성 주입(HeroService.ts)

    import { Component, OnInit } from '@angular/core';
    import { Hero } from '../hero';
    import { HeroService} from '../hero.service';
    
    @Component({
      selector: 'app-heroes',
      templateUrl: './heroes.component.html',
      styleUrls: ['./heroes.component.css']
    })
    export class HeroesComponent implements OnInit {
      heroes: Hero[];
    
      constructor(private heroService: HeroService) { }
    
      ngOnInit() {
        this.getHeroes();
      }
    
      getHeroes(): void {
        this.heroService.getHeroes()
          .subscribe(heroes => this.heroes = heroes);
      }
    }

 위 코드를 보면 HeroService의 인스턴스를 컴포넌트가 직접 생성하지 않습니다.
 
  이는 컴포넌트가 직접 의존관계 객체의 인스턴스를 생성하는 것이 아니라 Angular가 인스턴스를 생성하고 컴포넌트에 전달하는 방식이기 때문입니다. 컴포넌트는 필요한 의존 관계 객체를 요구하고, 프레임워크는 제어권(Control)을 갖는 주체로 동작하여 요구된 의존관계 객체의 인스턴스를 직접 생성하여 전달한다. 이를 **제어권의 역전(Inversion of Control, IoC)**이라 한다.
 
 컴포넌트는 더 이상 의존 관계 객체의 인스턴스 생성에 대해 관여하지 않아도 됩니다. Angular는 설정 정보에 의해 인스턴스를 생성하여 컴포넌트에게 전달(주입, Inject)해 줍니다. 이를 **의존성 주입(Dependency Injection)이라고** 합니다.



## 인젝터(Injector)
![injector](https://d2mxuefqeaa7sj.cloudfront.net/s_969374E9BAEFEA4D82372A0CBE238ECBB4F656CC8FEBECF933D2B171094D257E_1522218359167_image.png)



1.  컴포넌트가 생성될 때, Angular는 컴포넌트에 필요한 인스턴스를 인젝터에 요청합니다. 
2. 인젝터는 이전에 이미 생성한 인스턴스를 담고 있는 컨테이너를 관리하고 있습니다. 요청된 인스턴스가 컨테이너에 존재하지 않으면 인스턴스를 생성하고 컨테이너에 추가합니다. 
3. 요청된 인스턴스를 컴포넌트 생성자의 인자로 주입합니다.

 
 
 

## 인젝터 트리(Injector Tree)

컴포넌트는 트리 구조로 구성된다. 컴포넌트는 각각 하나의 인젝터를 가지고 있기 때문에 인젝터 트리는 컴포넌트의 트리 구조와 동일한 형태를 띄게 됩니다.


1. 컴포넌트의 주입 요청이 있을 때 인젝터는 현재 컴포넌트에서 등록한 프로바이더에서 주입 대상을 검색합니다. 
2. 이때 해당 컴포넌트의 프로바이더에서 주입 대상을 찾을 수 없으면 상위 컴포넌트의 프로바이더에서 주입 대상을 검색합니다. 
3. 상위 컴포넌트의 프로바이더를 검색하여 주입 대상을 찾으면 해당 인젝터는 인스턴스를 생성하며 **상위 인젝터가 생성한 인스턴스는 하위 컴포넌트에서 사용할 수 있습니다.**
4. 따라서 인젝터 트리의 최상위 인젝터 즉 루트 인젝터에서 생성한 인스턴스는 전역에서 사용 가능한 전역 서비스로 사용할 수 있습니다.




## 프로바이더(Provider)
![NgModule Provider](https://d2mxuefqeaa7sj.cloudfront.net/s_969374E9BAEFEA4D82372A0CBE238ECBB4F656CC8FEBECF933D2B171094D257E_1522218889170_image.png)
![Component Provider](https://d2mxuefqeaa7sj.cloudfront.net/s_969374E9BAEFEA4D82372A0CBE238ECBB4F656CC8FEBECF933D2B171094D257E_1522218932087_image.png)



- @NgModule 어노테이션에 등록한 서비스는 모듈 전체(루트 모듈인 경우, 애플리케이션 전역)에 반영됩니다.
- @Component 어노테이션에 등록한 서비스는 해당 컴포넌트와 자식 컴포넌트에 반영됩니다. 
- **모듈 레벨에 등록한 서비스는 하나의 인스턴스를 공유하지만 컴포넌트 레벨로 등록한 서비스는 컴포넌트가 생성될 때마다 새로운 인스턴스를 취득한다.**


1. 클래스 프로바이더
2. 프로퍼티 프로바이더
3. 팩토리 프로바이더





# What’s next 👩‍🍳 
----------



