# Template Syntax
## HTML in templates
* 템플릿 문법은 템플릿을 작성하기 위한 Angular 고유의 확장 표기법이다.
* 템플릿과 컴포넌트 클래스 간 데이터 공유를 위한 데이터 바인딩과 동적으로 DOM 구조, 스타일 등을 변경할 수 있는 빌트인 디렉티브 등을 지원한다.
* 정적인 뷰는 HTML만으로 정의할 수 있지만 컴포넌트와 연계하여 동적으로 변화하는 뷰를 정의하기 위해서 템플릿 문법을 사용한다.
* Angular가 제공하는 템플릿 문법은 아래와 같다.
    * 데이터 바인딩
        * 인터폴레이션(Interpolation)
        * 프로퍼티 바인딩(Property binding)
        * 어트리뷰트 바인딩(Attribute binding)
        * 클래스 바인딩(Class binding)
        * 스타일 바인딩(Style binding)
        * 이벤트 바인딩(Event binding)
        * 양방향 데이터 바인딩(Two-way binding)
    * 빌트인 디렉티브(Built-in directive)
    	* 빌트인 어트리뷰트 디렉티브(Built-in attribute directive)
            * ngClass
            * ngStyle
        * 빌트인 구조 디렉티브(Built-in structural directive)
            * ngIf
            * ngFor
			* ngSwitch
* 템플릿 참조 변수(Template reference variable)
* 템플릿 표현식 연산자(Template expression operator)
* http://poiemaweb.com/img/template.png

## Interpolation ( {﻿{...}} )
* 인터폴레이션을 통해 HTML 요소를 할당할 수 있다.
```javascript
<h3>
  {{title}}
  <img src="{{heroImageUrl}}" style="height:30px">
</h3>
```
* 계산식도 삽입할 수 있다. Angular가 먼저 평가를 한 후 문자열로 변환한다.
```javascript
<!-- "The sum of 1 + 1 is 2" -->
<p>The sum of 1 + 1 is {{1 + 1}}</p>
```
* 함수 호출도 가능하다.
```javascript
<!-- "The sum of 1 + 1 is not 4" -->
<p>The sum of 1 + 1 is not {{1 + 1 + getVal()}}</p>
```

## Template expressions
### Expression context
* 표현 문맥은 전형적으로 컴포넌트 인스턴스이다.
* 더블 중괄호 안에 있는 `title`이나 따옴표로 작성한 `isUnchaged`는 `AppComponent`의 속성을 참조한다.
```javascript
{{title}}
<span [hidden]="isUnchanged">changed</span>
```
* 또한 템플릿 입력 변수(let hero)나 템플릿 참조 변수(#heroInput)과 같은 템플릿 컨텍스트의 속성을 참조 할 수도 있다.
```
<div *ngFor="let hero of heroes">{{hero.name}}</div>
<input #heroInput> {{heroInput.value}}
```

### Expression guidelines
* 템플릿 표현은 어플리케이션을 만들거나 중단할 수 있다. 따라서 템플릿 표현식을 사용할 경우 다음 가이드를 생각하고 있어야한다.
* No visible side effects
    * 템플릿 표현은 어플리케이션의 상태를 바꾸면 안된다.
    * 이 규칙은 단방향 데이터 흐름 정책에 필수적이다.
    * 뷰는 단일 렌더링 단계에사 안정적이어야 한다.
* Quick execution
    * Angular는 변경 감지주기마다 템플릿 표현식을 실행한다.
    * 변경 감지주기는 Promise, http 결과, 타이머 이벤트, 키 누르기 및 마우스 이동과 같은 많은 비동기 활동에 의해 트리거됩니다.
    * 표현은 빠르게 끝나야하며, 특히 느린 기기의 경우 사용자 경험이 좋을 수 없다.
    * 계산 값이 비싼 경우 값 캐싱을 고려해야 한다.
* Simplicity
    * 템플릿 표현은 아주 복잡하게 작성할 수 있지만 이것은 피해야한다.
    * 비지니스 로직을 컴포넌트에서 작성하는 것으로 한정하는 것이 좋다. 개발 및 시험이 쉬워진다.

## Template statements
* 템플릿문은 컴포넌트나 지시자와 같은 바인딩 대상에서 발생하는 이벤트에 응답한다.
```javascript
<button (click)="deleteHero()">Delete hero</button>
```
* 템플릿 표현식과 마찬가지로 템플릿 문은 Javascript와 비슷한 언어를 사용한다.
* 기본할당(=)과 체인 표현식(; 또는 ,)을 모두 지원한다.
* 하지만 다음 구문은 허용되지 않는다.
    * new
    * ++, --
    * +=, -=
    * 비트연사자, |, &
* http://poiemaweb.com/img/databinding-changedetection.png

## Binding syntax
| 데이터 방향                        | 문법                                                              | 타입                                     |
|---------------------------------------|---------------------------------------------------------------------|------------------------------------------|
| 데이터 소스에서 뷰 타겟으로 단방향 | ```{{expression}} [target]="expression" bind-target="expression"``` | 보간, 프로퍼티, 어트리뷰트, 클래스, 스타일 |
| 뷰 타겟에서 데이터 소스로 단방향 | ```(target)="statement" on-target="statement"```                    | 이벤트                                    |
| 양방향                               | ```[(target)]="expression" bindon-target="expression"```            | 양방향                                  |
* HTML attribute vs. DOM property
```
The distinction between an HTML attribute and a DOM property is crucial to understanding how Angular binding works.

Attributes are defined by HTML. Properties are defined by the DOM (Document Object Model).

A few HTML attributes have 1:1 mapping to properties. id is one example.

Some HTML attributes don't have corresponding properties. colspan is one example.

Some DOM properties don't have corresponding attributes. textContent is one example.

Many HTML attributes appear to map to properties ... but not in the way you might think!

That last category is confusing until you grasp this general rule:

Attributes initialize DOM properties and then they are done. Property values can change; attribute values can't.

For example, when the browser renders <input type="text" value="Bob">, it creates a corresponding DOM node with a value property initialized to "Bob".

When the user enters "Sally" into the input box, the DOM element value property becomes "Sally". But the HTML value attribute remains unchanged as you discover if you ask the input element about that attribute: input.getAttribute('value') returns "Bob".

The HTML attribute value specifies the initial value; the DOM value property is the current value.

The disabled attribute is another peculiar example. A button's disabled property is false by default so the button is enabled. When you add the disabled attribute, its presence alone initializes the button's disabled property to true so the button is disabled.

Adding and removing the disabled attribute disables and enables the button. The value of the attribute is irrelevant, which is why you cannot enable a button by writing <button disabled="false">Still Disabled</button>.

Setting the button's disabled property (say, with an Angular binding) disables or enables the button. The value of the property matters.

The HTML attribute and the DOM property are not the same thing, even when they have the same name.
```
## Property binding ( [property] )
* Property binding or interpolation?
    * 보간은 많은 경우에 속성 바인딩에 대한 편리한 대안 입니다.
    * 데이터 값을 문자열로 렌더링 할 때 하나의 형식을 다른 형식보다 선호하는 기술적 이유는 없습니다.
    * 코딩 스타일 규칙을 수립하고 규칙을 준수하고 현재 작업에 가장 자연스러운 느낌을주는 양식을 선택하는 것이 좋습니다.
    * 요소 속성을 문자열이 아닌 데이터 값으로 설정하는 경우 속성 바인딩을 사용해야 합니다 .
* Remember the brackets
    * 괄호는 템플릿 표현식을 평가하기 위해 Angular에 지시한다.
    * 대괄호를 생략하면 Angular는 문자열을 상수로 처리하고 해당 문자열로 대상 속성 을 초기화 한다. 문자열을 평가 하지 않는다.
```javascript
<!-- ERROR: HeroDetailComponent.hero expects a
     Hero object, not the string "currentHero" -->
  <app-hero-detail hero="currentHero"></app-hero-detail>
```
* Content security
	* 보간은 속성 바인딩과 스크립트 태그를 다르게 처리하지만 두 방법 모두 내용을 무해하게 렌더링합니다.
```javascript
evilTitle = 'Template <script>alert("evil never sleeps")</script>Syntax';
...
<!--
  Angular generates warnings for these two lines as it sanitizes them
  WARNING: sanitizing HTML stripped some content (see http://g.co/ng/security#xss).
 -->
<p><span>"{{evilTitle}}" is the <i>interpolated</i> evil title.</span></p>
<p>"<span [innerHTML]="evilTitle"></span>" is the <i>property bound</i> evil title.</p>
```
