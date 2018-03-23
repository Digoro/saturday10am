# 3. 히어로 편집기
이제 응용 프로그램에 기본 제목이 있습니다. 다음으로 영웅 정보를 표시하고 해당 컴포넌트를 응용 프로그램에 배치 할 새 컴포넌트를 만듭니다.


## heroes 컴포넌트 만들기
----------

Angular CLI를 사용하여 heroes이라는 새로운 컴포넌트를 생성하십시오.


    > ng generate component heroes


CLI는 src / app / heroes /라는 새 폴더를 만들고 HeroesComponent의 세 파일을 생성합니다.

HeroesComponent 클래스 파일은 다음과 같습니다.

app/heroes/heroes.component.ts (initial version)

    import { Component, OnInit } from '@angular/core';
    
    @Component({
      selector: 'app-heroes',
      templateUrl: './heroes.component.html',
      styleUrls: ['./heroes.component.css']
    })
    export class HeroesComponent implements OnInit {
    
      constructor() { }
    
      ngOnInit() {
      }
    
    }


Angular 코어 라이브러리에서 항상 구성 요소 기호를 가져오고 @Component로 컴포넌트 클래스에 데코레이터를 추가합니다.

@Component는 컴포넌트의 앵귤러 메타 데이터를 지정하는 데코레이터 함수입니다.

CLI는 세 가지 메타 데이터 속성을 생성했습니다.

selector - 컴포넌트의 CSS 요소 선택자
templateUrl - 컴포넌트의 템플릿 파일 위치입니다.
styleUrls - 컴포넌트의 CSS 스타일의 주소.
CSS 요소 선택기 'app-heroes'는 상위 구성 요소의 템플릿에서이 컴포넌트를 식별하는 HTML 요소의 이름과 일치합니다.

ngOnInit은 라이프 사이클 함수입니다. Angular는 구성 요소를 만든 직후 ngOnInit을 호출합니다. 초기화 로직을 넣기 좋은 장소입니다.

AppModule처럼 다른 곳에서 사용할 수 있도록 항상 컴포넌트 클래스를 내보냅니다(export).





## 영웅 속성 추가
----------

"Windstorm"이라는 영웅을위한 HeroesComponent에 영웅 속성을 추가하십시오.

heroes.component.ts (hero property)

    hero = 'Windstorm';



## 영웅이름을 전시해보즈아아아
----------

heroes.component.html 템플릿 파일을 엽니다. Angular CLI에서 생성 된 기본 텍스트를 삭제하고 새로운 영웅 속성에 대한 데이터 바인딩으로 바꿉니다.

heroes.component.html

    {{hero}}




## HeroesComponent 전시해보즈아아아
----------

HeroesComponent를 표시하려면 이를  AppComponent의 템플릿에 추가해야합니다.
app-heroes는 HeroesComponent의 템플릿 이름(셀렉터)입니다. 타이틀 바로 아래에 템플릿을 추가해봅니다.

src/app/app.component.html

    <h1>{{title}}</h1>
    <app-heroes></app-heroes>

CLI에서 ng serve가 계속 실행중이라면 자동으로 템플릿이 추가된것을 확인할 수 있습니다.


# Hero 클래스 만들기
----------

히어로 클래스를 만들어 봅시다.

자신의 파일에 src / app 폴더에 Hero 클래스를 만듭니다. id 및 name 속성을 정해주십시오.

src/app/hero.ts

    export class Hero {
      id: number;
      name: string;
    }



HeroesComponent 클래스로 돌아와 Hero 클래스를 가져옵니다.

컴포넌트의 영웅 속성을 영웅 유형으로 리팩토링합니다. id를 1로하고 Windstorm으로 이름을 초기화하십시오.

수정 된 HeroesComponent 클래스 파일은 다음과 같아야합니다.


/app/heroes/heroes.component.ts

    import { Component, OnInit } from '@angular/core';
    import { Hero } from '../hero';
    
    @Component({
      selector: 'app-heroes',
      templateUrl: './heroes.component.html',
      styleUrls: ['./heroes.component.css']
    })
    export class HeroesComponent implements OnInit {
      hero: Hero = {
        id: 1,
        name: 'Windstorm'
      };
    
      constructor() { }
    
      ngOnInit() {
      }
    
    }


- 영웅을 문자열에서 클래스 객체로 변경했기 때문에 더 이상 페이지가 제대로 표시되지 않습니다.



## 영웅 객체 전시하기
----------

영웅의 이름을 알리고 다음과 같이 세부 레이아웃에 ID와 이름을 모두 보여주기 위해 템플릿의 바인딩을 업데이트하십시오.

heroes.component.html (HeroesComponent's template)

    <h2>{{ hero.name }} Details</h2>
    <div><span>id: </span>{{hero.id}}</div>
    <div><span>name: </span>{{hero.name}}</div>

브라우저가 새로 고쳐져 영웅의 정보가 표시됩니다.




## Uppercase Pipe 이용해보기
----------
    <h2>{{ hero.name | uppercase }} Details</h2>

브라우저가 새로 고쳐지고 이제 영웅의 이름이 대문자로 표시됩니다.

파이프 연산자 (|) 바로 뒤에있는uppercase는 내장 된 UppercasePipe를 활성화합니다.

파이프는 문자열, 통화 금액, 날짜 및 기타 디스플레이 데이터의 형식을 지정하는 좋은 방법입니다. 

내장 파이프를 이용할 수도 있고 커스텀 파이프를 만들 수도 있습니다.




# 영웅 편집하기
----------

사용자는 <input> 텍스트 상자에서 영웅 이름을 편집 할 수 있어야합니다.

텍스트 상자는 영웅의 이름과 속성을 표시하고 사용자가 입력 할 때 해당 속성을 업데이트해야합니다. 즉, 컴포넌트 클래스에서 화면으로, 그리고 화면에서 클래스로 데이터가 양방향으로 흐른다는 것을 확인할 수 있습니다.

데이터 흐름을 자동화하려면 <input> 양식 요소와 hero.name 속성 사이에 양방향 데이터 바인딩을 설정하십시오.


## 양방향 바인딩

HeroesComponent 템플릿의 세부 영역을 다음과 같이 리펙토링합니다.

src/app/heroes/heroes.component.html (HeroesComponent's template)

    <div>
        <label>name:
          <input [(ngModel)]="hero.name" placeholder="name">
        </label>
    </div>

[(ngModel)]은 Angular의 양방향 데이터 바인딩 구문입니다.

여기서 hero.name 속성을 HTML 텍스트 상자에 바인딩하여 hero.name 속성에서 textbox로 이동하고 textbox에서 hero.name으로 다시 이동할 수 있습니다.

하지만 양방향 바인딩을 그냥 사용하면 다음과 같은 에러가 발생합니다.

![](https://d2mxuefqeaa7sj.cloudfront.net/s_85078B58FF5DBBC41D6AFD5C29C41FEFAD450F94B1FF7A39B66408C8E66A45BE_1520947800796_image.png)


ngModel은 유효한 Angular 지시문이지만 기본적으로 사용할 수 없습니다.

그것은 선택적 FormsModule에 속하므로 이를 사용하도록 import 해야합니다.




## AppModule
----------

앵귤러는 응용 프로그램의 컴포넌트나 서비스 등의 조각들이 서로 잘 맞는지, 응용 프로그램에 필요한 다른 파일과 라이브러리가 있는지 알아야합니다. 이 정보를 메타 데이터라고합니다.

일부 메타 데이터는 컴포넌트 클래스에 추가 한 @Component 데코레이터에 있습니다. 다른 중요한 메타 데이터는 @NgModule 데코레이터에 있습니다.

가장 중요한 @NgModuledecorator는 최상위 AppModule 클래스에 주석을 추가합니다.

Angular CLI는 프로젝트를 만들 때 src / app / app.module.ts에 AppModule 클래스를 생성했습니다. 

여기에 이제 우리는 FormsModule을 추가합니다.



## Import *FormsModule*
----------

AppModule을 열고 FormsModule을 import 합니다. @angular/forms에서 import할 수 있습니다.

app.module.ts (FormsModule symbol import)

    import { FormsModule } from '@angular/forms'; // <-- NgModel lives here

그런 다음 FormsModule을 @NgModule 메타 데이터의 imports 배열에 추가합니다. 이 배열에는 응용 프로그램에 필요한 외부 모듈 목록이 들어 있습니다.

app.module.ts ( @NgModule imports)

    imports: [
      BrowserModule,
      FormsModule
    ],

브라우저가 새로 고침되면 앱이 다시 작동합니다. 영웅의 이름을 편집하고 텍스트 상자 위의 <h2>에 반영된 변경 사항을 즉시 볼 수 있습니다.




## HeroesComponent 선언
----------

모든 컴포넌트는 하나의 NgModule에 모두 선언되어야합니다.

아직 HeroesComponent를 선언하지 않았습니다. 그렇다면 왜 프로그램은 잘 작동할까요?

그것은 Angular CLI가 AppModule에서 HeroesComponent를 생성했을 때이를 선언했기 때문에 작동했습니다.

src / app / app.module.ts를 열고 상단 근처에서 HeroesComponent를 찾으십시오.


    import { HeroesComponent } from './heroes/heroes.component';


    declarations: [
      AppComponent,
      HeroesComponent
    ],





