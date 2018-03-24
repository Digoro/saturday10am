# 1. Quick Start
좋은 도구를 사용하면 모든 것을 손으로 다룬 것보다 응용 프로그램 개발을보다 빠르고 쉽게 유지 관리 할 수 있습니다.

Angular CLI는 프로젝트를 만들고 파일을 추가하며 테스트, 번들링 및 배포와 같은 다양한 개발 작업을 수행 할 수 있는 명령 도구입니다.

이 가이드의 목표는 Angular 프로젝트를 사용하는 Style Guide 권장 사항을 준수하면서 Angular CLI를 사용하여 TypeScript에서 간단한 Angular 응용 프로그램을 작성하고 실행하는 것입니다.

이 장의 끝 부분에서는 CLI를 사용하여 개발에 대한 기본 지식을 얻게되며 이 샘플은 실제 응용 프로그램의 기초가됩니다.

그리고 [예제를 다운로드](https://angular.io/generated/zips/cli-quickstart/cli-quickstart.zip)할 수도 있습니다.


## Step 1. 개발 환경 구성

당신은 무엇이든하기 전에 개발 환경을 설정해야합니다.

Node.js® 및 npm이 아직 시스템에 설치되어 있지 않은 경우 설치하십시오.

터미널 / 콘솔 창에서 node -v 및 npm -v를 실행하여 적어도 노드 6.9.x 및 npm 3.x.x가 설치되어 있는지 확인하십시오. 이전 버전에서는 오류가 발생하지만 최신 버전에서는 문제가 없습니다.


Then **install the** [**Angular CLI**](https://github.com/angular/angular-cli) globally.

    > npm install -g @angular/cli




## Step 2. 새 프로젝트 만들기

새 프로젝트 만들기

    > ng new my-app


- 새 프로젝트를 만드는 데 다소 시간이 걸립니다.



## Step 3. 어플리케이션 실행하기

프로젝트 루트 폴더에서 실행 가능합니다.

    > cd my-app
    > ng serve --open

ng serve 명령은 서버를 시작하고 파일을 감시하며 해당 파일을 변경할 때 응용 프로그램을 다시 작성합니다.

--open (또는 just -o) 옵션을 사용하면 http : // localhost : 4200 /주소로 브라우저가 자동으로 열립니다.




![](https://d2mxuefqeaa7sj.cloudfront.net/s_D2C06DF1F17F83CA781AB56FF3AC8B0C4363EDBEE73588CF551B03DF4E8B06DE_1520762681028_image.png)




## Step 4. 첫 번째 컴포넌트 수정해보기

CLI가 첫 번째 Angular 컴포넌트를 작성했습니다. 이것은 루트 컴포넌트이며 app-root라고합니다. ./src/app/app.component.ts에서 찾을 수 있습니다.

컴포넌트 파일을 열고 title 속성을 'app'에서 'My First Angular App!'으로 변경하십시오.

src/app/app.component.ts

    export class AppComponent {
      title = 'My First Angular App!';
    }

브라우저는 수정 된 제목으로 자동으로 다시 로드됩니다. 

src / app / app.component.css를 열고 컴포넌트에 스타일을 추가하십시오.


src/app/app.component.css

    h1 {
      color: #369;
      font-family: Arial, Helvetica, sans-serif;
      font-size: 250%;
    }





## 다음 할 일~ 😃 

Tour of Heroes Tutorial  애플리케이션을 만들 준비가되었습니다.

또는 새로운 프로젝트의 파일에 대해 더 배울 수 있습니다.



## 프로젝트 파일 개요

Angular CLI 프로젝트는 빠른 실험과 엔터프라이즈 솔루션의 기초입니다.

확인해야 하는 첫 번째 파일은 README.md입니다. 여기에는 CLI 명령을 사용하는 방법에 대한 몇 가지 기본 정보가 있습니다. Angular CLI가 작동하는 방식에 대해 더 알고 싶다면 Angular CLI 저장소([the Angular CLI repository](https://github.com/angular/angular-cli)) 및 Wiki([Wiki](https://github.com/angular/angular-cli/wiki))를 방문하십시오.

생성 된 파일 중 일부는 생소 할 수 있습니다.




## Src 폴더

 당신의 응용 프로그램은 src 폴더에 있습니다. 모든 앵귤러 요소, 템플릿, 스타일, 이미지 및 앱에 필요한 모든 항목이 여기에 있습니다. 이 폴더 외부의 모든 파일은 앱 구축을 지원하기위한 것입니다.


![](https://d2mxuefqeaa7sj.cloudfront.net/s_D2C06DF1F17F83CA781AB56FF3AC8B0C4363EDBEE73588CF551B03DF4E8B06DE_1520763190764_image.png)





| **File**                                | **Purpose**                                                                                                                                                                                                                                                                                                                                                                                                      |
| --------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| app/app.component.{ts,html,css,spec.ts} | Defines the `AppComponent` along with an HTML template, CSS stylesheet, and a unit test. It is the **root** component of what will become a tree of nested components as the application evolves.                                                                                                                                                                                                                |
| app/app.module.ts                       | Defines `AppModule`, the [root module](https://angular.io/guide/bootstrapping) that tells Angular how to assemble the application. Right now it declares only the `AppComponent`. Soon there will be more components to declare.                                                                                                                                                                                 |
| assets/*                                | A folder where you can put images and anything else to be copied wholesale when you build your application.                                                                                                                                                                                                                                                                                                      |
| environments/*                          | This folder contains one file for each of your destination environments, each exporting simple configuration variables to use in your application. The files are replaced on-the-fly when you build your app. You might use a different API endpoint for development than you do for production or maybe different analytics tokens. You might even use some mock services. Either way, the CLI has you covered. |
| favicon.ico                             | Every site wants to look good on the bookmark bar. Get started with your very own Angular icon.                                                                                                                                                                                                                                                                                                                  |
| index.html                              | The main HTML page that is served when someone visits your site. Most of the time you'll never need to edit it. The CLI automatically adds all `js` and `css` files when building your app so you never need to add any `<script>` or `<link>` tags here manually.                                                                                                                                               |
| main.ts                                 | The main entry point for your app. Compiles the application with the [JIT compiler](https://angular.io/guide/glossary#jit) and bootstraps the application's root module (`AppModule`) to run in the browser. You can also use the [AOT compiler](https://angular.io/guide/aot-compiler) without changing any code by appending the`--aot` flag to the `ng build` and `ng serve` commands.                        |
| polyfills.ts                            | Different browsers have different levels of support of the web standards. Polyfills help normalize those differences. You should be pretty safe with `core-js` and `zone.js`, but be sure to check out the [Browser Support guide](https://angular.io/guide/browser-support) for more information.                                                                                                               |
| styles.css                              | Your global styles go here. Most of the time you'll want to have local styles in your components for easier maintenance, but styles that affect all of your app need to be in a central place.                                                                                                                                                                                                                   |
| test.ts                                 | This is the main entry point for your unit tests. It has some custom configuration that might be unfamiliar, but it's not something you'll need to edit.                                                                                                                                                                                                                                                         |
| tsconfig.{app|spec}.json                | TypeScript compiler configuration for the Angular app (`tsconfig.app.json`) and for the unit tests (`tsconfig.spec.json`).                                                                                                                                                                                                                                                                                       |





## 루트 폴더

src / 폴더는 프로젝트의 루트 폴더에있는 항목 중 하나입니다. 다른 파일은 응용 프로그램을 빌드, 테스트, 유지 관리, 문서화 및 배포하는 데 도움이됩니다. 이 파일들은 src / 옆의 루트 폴더에 있습니다.


![](https://d2mxuefqeaa7sj.cloudfront.net/s_D2C06DF1F17F83CA781AB56FF3AC8B0C4363EDBEE73588CF551B03DF4E8B06DE_1520763299035_image.png)




| **File**           | **Purpose**                                                                                                                                                                                                                                     |
| ------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| e2e/               | Inside `e2e/` live the end-to-end tests. They shouldn't be inside `src/` because e2e tests are really a separate app that just so happens to test your main app. That's also why they have their own `tsconfig.e2e.json`.                       |
| node_modules/      | Node.js creates this folder and puts all third party modules listed in package.json inside of it.                                                                                                                                               |
| .angular-cli.json  | Configuration for Angular CLI. In this file you can set several defaults and also configure what files are included when your project is built. Check out the official documentation if you want to know more.                                  |
| .editorconfig      | Simple configuration for your editor to make sure everyone that uses your project has the same basic configuration. Most editors support an `.editorconfig` file. See [http://editorconfig.org](http://editorconfig.org/) for more information. |
| .gitignore         | Git configuration to make sure autogenerated files are not commited to source control.                                                                                                                                                          |
| karma.conf.js      | Unit test configuration for the [Karma test runner](https://karma-runner.github.io/), used when running `ng test`.                                                                                                                              |
| package.json       | npm configuration listing the third party packages your project uses. You can also add your own custom scripts here.                                                                                                                            |
| protractor.conf.js | End-to-end test configuration for [Protractor](http://www.protractortest.org/), used when running `ng e2e`.                                                                                                                                     |
| README.md          | Basic documentation for your project, pre-filled with CLI command information. Make sure to enhance it with project documentation so that anyone checking out the repo can build your app!                                                      |
| tsconfig.json      | TypeScript compiler configuration for your IDE to pick up and give you helpful tooling.                                                                                                                                                         |
| tslint.json        | Linting configuration for [TSLint](https://palantir.github.io/tslint/) together with [Codelyzer](http://codelyzer.com/), used when running `ng lint`. Linting helps keep your code style consistent.                                            |


