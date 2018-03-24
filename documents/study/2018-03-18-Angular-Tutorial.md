# Angular Tutorial😵 18/03/17


# Heroes Tutorial 👻 
----------
## [튜토리얼 목표](https://angular.io/tutorial) 

다음과 같은 앵귤러의 구성 요소들을 사용해보즈아아아 🤗 


1. 내장된 **Angular 지시자**를 사용하여 요소를 표시하거나 숨기고 영웅 데이터 목록을 표시합니다.
2. 영웅의 세부 사항을 표시하고 영웅의 배열을 표시하는 앵귤러 컴포넌트를 만듭니다.
3. 읽기 전용 데이터에 **단방향 데이터 바인딩**을 사용하십시오.
4. 편집 가능한 필드를 추가하여 **양방향 데이터 바인딩**으로 모델을 업데이트하십시오.
5. **키 입력 및 클릭과 같은 사용자 이벤트**에 구성 요소 메서드를 바인딩합니다.
6. 사용자가 마스터 목록에서 영웅을 선택하고 세부보기에서 해당 영웅을 편집 할 수 있습니다.
7. **파이프**로 데이터를 포맷하십시오.
8. 영웅을 모으는 **공유 서비스**를 만듭니다.
9. ~~**라우팅**~~~~을 사용하여 여러보기와 해당 구성 요소를 탐색합니다.~~






# Angular CLI 🎃 
----------
## CLI 설치
    > npm install -g @angular/cli


## 프로젝트 생성
    > ng new my-project


## 서버 가동
    > ng serve

--open(o) 옵션을 사용하면 서버 가동할 때 브라우저를 같이 실행할 수 있다.



## Angular 구성 요소 생성



    > ng generate(ng g)

 

![](https://d2mxuefqeaa7sj.cloudfront.net/s_4F50C11AA730854A8437FF198333CC186BB6DCD6BE67EEF915014B3CFEC76D27_1521174036175_image.png)


Component, Directive, Pipe, Service 생성 가능


    ex) ng generate component My-Component —flat

--flat 옵션을 사용하면 명령어 실행 디렉토리 레벨에서 폴더 생성하지 않고 구성요소 생성이 가능하다.





# Angular 기본 파일 구조 🙈 
----------
![](https://d2mxuefqeaa7sj.cloudfront.net/s_4F50C11AA730854A8437FF198333CC186BB6DCD6BE67EEF915014B3CFEC76D27_1521175054311_image.png)

- **src/index.html** : 앵귤러 실행 시 실행되는 루트 페이지이다. 외부 라이브러리나 내부모듈을 이 페이지에 import하여 사용한다.
- **src/style.css** : global css style이 저장되는 디렉토리이다.
- **src/assets** : 그림파일이나 외부 라이브러리를 저장하는 용도로 사용된다.
- **src/environments** : enviroment.prod.ts와 environment.ts의 파일이 있는데, 개발하는 웹의 실행환경이 여러가지 있다면 실행환경(개발용, 출판용, 테스트용)에 따라 다른 값을 주고 싶을때 사용한다. 일반적으로 ng serve로 실행할 때는 environment.ts의 내용을 읽어서 실행한다.
- **src/polyfills.ts :** 브라우저마다 지원하는 웹 표준이 다르기 때문에 브라우저마다의 차리를 표준화 해주는 데 사용하는 파일이다. core.js 및 zone.js로 인해 대부분 해결되지만 더 자세한 사항이 알고 싶다면  [Browser Support guide](https://angular.io/guide/browser-support)를 참고하면 된다.



**index.html**

![](https://d2mxuefqeaa7sj.cloudfront.net/s_4F50C11AA730854A8437FF198333CC186BB6DCD6BE67EEF915014B3CFEC76D27_1521181510208_image.png)






# Module 💩
----------

앵귤러의 주요 패키지

![](https://d2mxuefqeaa7sj.cloudfront.net/s_4F50C11AA730854A8437FF198333CC186BB6DCD6BE67EEF915014B3CFEC76D27_1521187654463_image.png)

- 모듈을 작성한 후 export 키워드를 사용하여 간편하게 외부로 export 할 수 있다.


## AppModule

Angular Application의 최상위 모듈로 모듈 구성을 총괄하는 컨트롤 타워 역할을 한다.

@NgModule(){}` 데코레이터를 사용하여 **imports(호출한 모듈), providers(서비스 주입), declarations(사용자 컴포넌트, 지시자, 파이프). bootstrap(구동할 컴포넌트)** 등을 명시한다.


![AppModule 😱](https://d2mxuefqeaa7sj.cloudfront.net/s_4F50C11AA730854A8437FF198333CC186BB6DCD6BE67EEF915014B3CFEC76D27_1521187874373_image.png)

- Angular 가 브라우저 위에서 작동하려면 BrowserModule 가 필수로 import되어야 한다.
- 양방향 바인딩을 사용하기 위해서는 FormsModule을 import해야 한다.








# 컴포넌트 🤫 
----------

Angular는 컴포넌트 기반의 프로그래밍이다. 컴포넌트는 외부 의존성 없이 동작 가능한 하나의 독립적인 프로그램이라고 볼 수 있다.

컴포넌트는 크게 Import 영역, 데코레이터 영역, Content 영역으로 나눌 수 있다.





# 서비스 🧟‍♀️ 
----------

Angular 서비스의 가장 큰 역할은 개별 컴포넌트들의 기능과 전체 어플리케이션 공통 기능의 분리라고 할 수 있다.


- 컴포넌트에 공통적으로 쓰일 수 있는 기능을 서비스로 만들어야 한다. 
- 중복되는 코드를 서비스로 옮기는 작업을 통해 컴포넌트의 응집성을 높일 수 있다.
- ex) 데이터 서비스, 로깅 서비스, 비즈니스 로직 서비스

또한, Angular Service는 컴포넌트 사이에서 데이터 중계자의 역할도 할 수 있다.


- 컴포넌트 to 컴포넌트 의 데이터 교환은 서비스를 통해 이루어 진다.
- @Input 데코레이터나 EventEmitter 객체를 이용하여 개별적인 속성 값을 주고 받을 수 있다.



    > ng g service service_name

위의 명령을 통하여 서비스를 생성할 수 있다.


간단한 Hello Service 예제를 통해 서비스에 대해 고찰해 봅시다.


## Hello Service 정의
    import { Injectable } from '@angular/core';
    
    @Injectable()
    export class HelloService {
      constructor() {  }
    
      say() {
        return "Hello Sydeny!!!"
      }
    }


## Hello Service AppModule에 등록
  Service를 이용하기 위해서는 사용하려고 하는 외부 클래스에서 의존성 주입(Dependency Injection)을 해야 하고 AppModule에서 서비스를 import한 후 provider로 등록을 해주어야 한다.
    import { BrowserModule } from '@angular/platform-browser';
    import { NgModule } from '@angular/core';
    import { AppComponent } from './app.component';
    import { HelloService } from './hello.service';
    
    @NgModule({
      declarations: [ AppComponent ],
      imports: [ rowserModule ],
      providers: [ HelloService ],
      bootstrap: [ AppComponent ]
    })
    export class AppModule { }



## AppComponent에서 Hello Service 사용
   AppComponent에서 Hello Service를 사용하기 위해서 서비스를 생성자를 통하여 주입하여 준다. 생성자를 통하여 초기화하는 것 이외에도 new 키워드를 사용하여 초기화하는 것도 가능하지만 객체 공유 문제 및 메모리 관련 문제가 생길 수 있다.(생성자를 통해 생성하면 Singleton 기법으로 생성된다.)
    import { Component } from '@angular/core';
    import { HelloService } from './hello.service'
    
    @Component({
      selector: 'app-root',
      templateUrl: './app.component.html',
      styleUrls: ['./app.component.css']
    })
    export class AppComponent {
      title = '';
      constructor(private helloService : HelloService) {
        this.title = helloService.say();
      }




## Heroes 튜토리얼 HeroService
  데이터 객체 전달용으로 사용
    getHeroes(): void {
      this.heroes = this.heroService.getHeroes();
    }






# Pipe 🧟‍♂️ 
----------

Pipe는 템플릿에서 값을 표시할 때 사용하는 일종의 **포맷터**라고 생각할 수 있다.


HTML 마크업 상에서 변환하고자 하는 데이터에 다음과 같은 형태로 사용한다. 

- 다른 Pipe를 연결해서 사용가능하고, 옵션은 콜론(:)을 연결해서 사용


    {{ value | PipeName : customOption1 :  customOption2 }}
    {{ value | Pipe1 | Pipe2 }}

**ex)**

    <p>오늘은 {{ today | date:“yyyy.MM.dd”}} 입니다.<p> 
    // input) today = Sun Apr 16 2017 17:35:39 GMT+0900 (KST)
    // output) 오늘은 2017.4.16 입니다
    
    <p>{{ text | slice:0:3 | uppercase }}</p>
    // input) text = 'abcdefghijk'
    // output) 'ABC'




## 내장 파이프

[Angular Doc API Reference](https://angular.io/docs/ts/latest/api/#!?query=pipe)에서 Pipe를 검색하면 내장 Pipe에 대한 정보를 확인할 수 있다.


![](https://d2mxuefqeaa7sj.cloudfront.net/s_4F50C11AA730854A8437FF198333CC186BB6DCD6BE67EEF915014B3CFEC76D27_1521178923425_image.png)


내장 파이프에 대한 코드를 확인하고 싶다면  [내장 파이프 코드](https://github.com/angular/angular/tree/09d9f5fe54e7108c47de61393e10712f8239d824/packages/common/src/pipes)에서 확인할 수 있다.

앵귤러JS에서 목록을 필터링하고 정렬하던 Filter, OrderBy 파이프는 성능이 좋지 않기 때문에 삭제되었다.




## 커스텀 Pipe 작성

입력값을 설정한 limit 값 까지만 표현하고 나머지는 …으로 표현하는 Pipe를 작성해본다.


    TypeScript (shorten.pipe.ts)
    import { Pipe, PipeTransform } from ‘@angular/core’;
    @Pipe(){
        name: 'shorten'
    }
    
    export class ShortenPipe implements PipeTransform {
      transform(value: any, limit: number) {    
        if (value.length > limit) {      
          return value.substr(0, limit) + ' ...';    
        }    
        return value;  
      }
    }

@Pipe() 데코레이터를 이용하여 name과 pure에 관한 속성을 설정해준다. pure 속성의 경우 false인 경우에만 입력하면 된다.

PipeTransform의 transform 메소드를 통해서 value와 limit 값을 입력받는다.

입력 값이 limit보다 큰 경우 문자열을 자르고 …을 붙여 return 해준다.




## Pure 속성

Pipe에는 pure라는 속성이 있다. pure와 impure의 두 가지 카테고리로 분류할 수 있는데, @Pipe() 데코레이터의 pure 설정 값(true or false)을 통해 나타낸다.

pure의 경우 primitive 변수가 입력값으로 들어올 경우에만 감지하는 파이프를 의미한다.

impure의 경우 모든 변경사항에 대해 감시하기 위해 수 밀리초마다 감지를 하기 때문에 남용되는 impure pipe는 서버에 안좋은 영향을 미칠 수 있다. 대표적인 예로 위에서 언급한 AngularJS의 Filter와 OrderBy 파이프가 있다. 




