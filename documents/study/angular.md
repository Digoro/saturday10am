# 데이터 전시(Displaying Data)
## 인터폴레이션
* 인터폴레이션(`interpolation`)으로 컴포넌트 요소(`property`) 전시
* 컴포넌트 속성을 전시하는 가장 쉬운 방법은 인터폴레이션을 통해 요소를 바인딩하는 것이다.
* 템플릿에서 중괄호 두 개로 감싸면 바인딩이 된다.
```javascript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `
    <h1>{{title}}</h1>
    <h2>My favorite hero is: {{myHero}}</h2>
    `
})
export class AppComponent {
  title = 'Tour of Heroes';
  myHero = 'Windstorm';
}
```
## 백틱
* ECMAScript 2015 부터 백틱(`)을 이용한 다중라인 문자를 지원한다.
```javascript
template: `
  <h1>{{title}}</h1>
  <h2>My favorite hero is: {{myHero}}</h2>
```
* 템플릿 정의
  * 컴포넌트 데코레이터에 `templateUrl` 혹은 `template`로 템플릿을 정의할 수 있다.
  * `templateUrl`은 컴포넌트 파일과 분리된 별개의 템플릿 파일의 경로를 지정한다.
  * `it` 옵션을 주면 별개의 템플릿 파일을 생성하지 않는다.(inline template)
```javascript
ng generate component hero -it
```
## *ngFor
* `*ngFor` 지시자를 이용하여 리스트의 내용을 전시한다.
```javascript
template: `
  <h1>{{title}}</h1>
  <h2>My favorite hero is: {{myHero}}</h2>
  <p>Heroes:</p>
  <ul>
    <li *ngFor="let hero of heroes">
      {{ hero }}
    </li>
  </ul>
`
```
## 클래스 정의
* 클래스 생성
```javascript
ng generate class hero
```
* 클래스 정의
  * 언뜻 보기에는 클래스는 프로퍼티를 가지지 않은 것처럼 보인다. 하지만 그렇지 않다.
  * 타입스크립트는 생성자 인자에 선언한 파라미터가 해당 클래스의 프로퍼티가 된다.
  * 정의 방법
    * 생성자 파라미터와 타입을 선언한다.
    * 동일한 이름의 `public` 프로퍼티를 선언한다.
    * 클래스의 인스턴스가 만들어질 때 상응되는 프로퍼티를 초기화하게 된다.
```javascript
export class Hero {
  constructor(
    public id: number,
    public name: string) { }
}
```
## *ngIf
* ture, flase 조건에 따라 엘리먼트를 삽입 혹은 제거 하는 지시자이다.
```javascript
<p *ngIf="heroes.length > 3">There are many heroes!</p>
```
