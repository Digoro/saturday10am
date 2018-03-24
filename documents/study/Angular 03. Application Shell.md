# 2. 프로젝트 생성

## 어플리케이션(프로젝트) 생성
----------

Angular CLI를 이용해 새 프로젝트를 생성합니다.


    > new angular-tour-of-heroes




## 어플리케이션 실행
----------

프로젝트 루트 폴더로 이동해 어플리케이션을 실행합니다.


    > cd angular-tour-of-heroes
    > ng serve --open






## Angular 컴포넌트
----------

표시되는 페이지는 응용 프로그램 Shell입니다. Shell은 AppComponent라는 Angular 컴포넌트에 의해 제어됩니다.

는 각도 응용 프로그램의 기본 구성 요소입니다. 화면에 데이터를 표시하고 사용자 입력을 수신하며 해당 입력을 기반으로 조치를 취합니다.




## 응용 프로그램 제목 변경
----------

좋아하는 편집기 또는 IDE에서 프로젝트를 열고 src / app 폴더로 이동하십시오.

세 개의 파일에 걸쳐 배포 된 셸 AppComponent의 구현을 확인할 수 있습니다.

app.component.ts - TypeScript로 작성된 컴포넌트 클래스 코드입니다.
app.component.html - HTML로 작성된 컴포넌트 템플릿
app.component.css - 컴포넌트의 CSS 스타일
컴포넌트 클래스 파일 (app.component.ts)을 열고 title 속성의 값을 'Tour of Heroes'로 변경하십시오.

app.component.ts (class title property)

    > title = 'Tour of Heroes';



app.component.html (template)

    > <h1>{{title}}</h1>

이중 중괄호는 Angular의 바인딩 구문입니다. 이 바인딩은 HTML 헤더 태그 안에 구성 요소의 title 속성 값을 제공합니다.

브라우저가 새로 고쳐지고 새 응용 프로그램 제목이 표시됩니다.



## CSS 적용
----------

src/styles.css (excerpt)

    /* Application-wide Styles */
    h1 {
      color: #369;
      font-family: Arial, Helvetica, sans-serif;
      font-size: 250%;
    }
    h2, h3 {
      color: #444;
      font-family: Arial, Helvetica, sans-serif;
      font-weight: lighter;
    }
    body {
      margin: 2em;
    }
    body, input[text], button {
      color: #888;
      font-family: Cambria, Georgia;
    }
    /* everywhere else */
    * {
      font-family: Arial, Helvetica, sans-serif;
    }

대부분의 응용 프로그램은 응용 프로그램에서 일관된 모양을 유지하려고 노력합니다. CLI는이 목적을 위해 빈 styles.css를 생성했습니다. 거기에 응용 프로그램 전체 스타일을 배치하십시오.

다음은 Tour of Heroes 샘플 앱의 styles.css에서 발췌 한 내용입니다.




