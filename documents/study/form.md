# Form
> *웹 서비스를 개발하면서 가장 많은 시간이 소요되는 부분이 입력 폼과 유효성 검증이였다.
Angular에서는 FormsModule과 ReactiveFomrsModule을 통해 이를 쉽게 개발하고 유지보수성이 높도록 하였다.
이 외에도 Formly, Ngx-Errors등과 같은 서드파티 모듈을 이용하여 좀 더 수려한 화면을 구성할 수 있다.*

* [Reactive Forms](#reactive-forms)
* [FormControl](#formcontrol)
* [FormArray](#formarray)
* [Built-In Validator](#built-in-validator)
* [Custom Validator](#custom-validator)
* [Formly](#formly)
* [Ngx Errors](#ngx-errors)


## Reactive Forms
* 리액티브 폼(모델 기반 폼)은 컴포넌트 클래스에서 폼 요소의 값 및 유효성 검증 상태를 관리하는 객체인 폼 모델(FormGroup, FormControl, FormArray)을 직접 정의/생성한다.   
* 그리고 form* 접두사가 붙은 디렉티브(formGroup, formGroupName, formControlName, formArrayName)를 사용하여 템플릿의 폼 요소와 폼 모델을 프로퍼티 바인딩으로 연결한다.
* 다시 말해 컴포넌트 클래스 내부에서 정의/생성한 폼 모델에 직접 접근하여 데이터 모델을 폼 모델에 반영하고 템플릿의 폼 컨트롤 요소의 상태 변화를 관찰(observe)하고 변화에 대응한다.  
* 리액티브 폼은 FormControl, FormGroup, FormArray 클래스를 중심으로 동작한다. 이들을 사용하기 위해서 @angular/forms 패키지의 ReactiveFormsModule을 애플리케이션 모듈에 추가한다.  

```javascript
// app.module.ts
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { ReactiveFormsModule } from '@angular/forms';

import { AppComponent } from './app.component';

@NgModule({
  declarations: [AppComponent],
  imports: [BrowserModule, ReactiveFormsModule],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```
## FormGroup 클래스와 formGroup/formGroupName 디렉티브
* FormGroup 인스턴스는 자신의 자식인 FormControl 인스턴스 또는 FormArray 인스턴스들을 그룹화하여 관리하기 위한 최상위 컨테이너이다.  
* FormControl 또는 FormArray 인스턴스와 같은 자식 폼 모델 인스턴스들을 하나의 객체로 그룹화하여 모든 자식 폼 모델 인스턴스의 값과 유효성 상태를 관리한다.  
* 만약 유효성을 검증할 때 자식 폼 모델 인스턴스 중 하나라도 유효하지 않다면 FormGroup은 유효하지 않게 된다.  
* 컴포넌트 클래스에 FormGroup 인스턴스를 직접 생성하고 formGroup 디렉티브를 사용하여 FormGroup 인스턴스와 폼 요소를 바인딩한다.  

```javascript
// app.component.ts
import { Component, OnInit } from '@angular/core';
import { FormGroup } from '@angular/forms';

@Component({
  selector: 'app-root',
  template: `
    <form [formGroup]="userForm" novalidate></form>
  `
})
export class AppComponent implements OnInit {

  userForm: FormGroup;

  ngOnInit() {
    this.userForm = new FormGroup({});
    console.log(this.userForm);
  }
}
```
## FormControl
* FormControl 인스턴스는 폼을 구성하는 기본 단위로서 폼 컨트롤 요소의 값이나 유효성 검증 상태를 추적하고 뷰와 폼 모델을 동기화된 상태로 유지한다.  
* 컴포넌트 클래스에서 FormControl 인스턴스를 직접 생성하고 formControlName 디렉티브를 사용하여 FormControl 인스턴스와 폼 컨트롤 요소를 바인딩한다.  

```javascript
import { Component, OnInit } from '@angular/core';
import { FormGroup, FormControl } from '@angular/forms';

@Component({
  selector: 'app-root',
  template: `
    <form [formGroup]="userForm" novalidate>
      <div>
        <input type="text" formControlName="userid" placeholder="user id">
      </div>
      <div formGroupName="passwordGroup">
        <div>
          <input type="password" formControlName="password" placeholder="password">
        </div>
        <div>
          <input type="password" formControlName="confirmPassword" placeholder="confirm password">
        </div>
      </div>
    </form>
    <pre>{{ userForm.value | json }}</pre>
    <pre>{{ userForm.status }}</pre>
  `
})
export class AppComponent implements OnInit {

  userForm: FormGroup;

  ngOnInit() {
    this.userForm = new FormGroup({
      userid: new FormControl(''),
      passwordGroup: new FormGroup({
        password: new FormControl(''),
        confirmPassword: new FormControl('')
      })
    });
    console.log(this.userForm);
  }
}
```

## FormArray
* FormArray 인스턴스는 자바스크립트의 배열과 유사하게 FormControl 인스턴스들을 그룹화하여 관리한다. FormArray는 폼 컨트롤 요소가 동적으로 생성되어 그 갯수가 변화할 때 사용한다.  
* formArrayName 디렉티브는 FormArray 인스턴스를 DOM 요소에 바인딩한다.  

```javascript
import { Component, OnInit } from '@angular/core';
import { FormGroup, FormControl, FormArray } from '@angular/forms';

@Component({
  selector: 'app-root',
  template: `
    <form [formGroup]="userForm" novalidate>
      <div formArrayName="hobbies">
        <div *ngFor="let hobby of hobbies.controls; let i=index">
          <input type="text" [formControlName]="i">
        </div>
      </div>
    </form>
    <pre>{{ userForm.value | json }}</pre>
    <pre>{{ userForm.status }}</pre>
  `
})
export class AppComponent implements OnInit {

  userForm: FormGroup;

  ngOnInit() {
    this.userForm = new FormGroup({
      hobbies: new FormArray([
        new FormControl(''),
        new FormControl('')
      ])
    });
    console.log(this.userForm);
  }
}
```

## Built-In Validator
* 템플릿 기반 폼은 유효성 검증이 필요한 템플릿의 폼 컨트롤 요소에 required, pattern과 같은 빌트인 검증기(Built-in validator)를 선언한다. 
* 리액티브 폼에서 사용 가능한 빌트인 검증기는 Validators 클래스에 정적 메소드로 정의되어 있다.  
```javascript
class Validators {
  static min(min: number): ValidatorFn
  static max(max: number): ValidatorFn
  static required(control: AbstractControl): ValidationErrors|null
  static requiredTrue(control: AbstractControl): ValidationErrors|null
  static email(control: AbstractControl): ValidationErrors|null
  static minLength(minLength: number): ValidatorFn
  static maxLength(maxLength: number): ValidatorFn
  static pattern(pattern: string|RegExp): ValidatorFn
  static nullValidator(c: AbstractControl): ValidationErrors|null
  static compose(validators: (ValidatorFn|null|undefined)[]|null): ValidatorFn|null
  static composeAsync(validators: (AsyncValidatorFn|null)[]): AsyncValidatorFn|null
}
```
## Custom validator
* 빌트인 검증기는 사용이 간편하지만 기본적인 검증 기능만을 제공하므로 복잡한 애플리케이션의 요구 사항을 충족시키기 어려운 경우가 있다.  
* Angular는 사용자 정의 검증기를 정의할 수 있으며 템플릿 기반 폼과 리액티브 폼 모두에 사용할 수 있다.  

```javascript
// password-validator.ts
import { AbstractControl } from '@angular/forms';

export class PasswordValidator {

  static match(form: AbstractControl) {
    const password = form.get('password').value;
    const confirmPassword = form.get('confirmPassword').value;

    if (password !== confirmPassword) {
      return { match: { password, confirmPassword }};
    } else {
      return null;
    }
  }
}
```

* 사용자 정의 검증기는 클래스의 정적 메소드로 정의한다. 이때 메소드의 매개변수는 검증 대상 폼 모델이다.  
* PasswordValidator 클래스의 정적 메소드 match는 패스워드와 확인 패스워드를 입력하는 폼 컨트롤 요소를 그룹화한 FormGroup의 인스턴스 passwordGroup에 적용할 것이기 때문에 매개변수 타입을 AbstractControl로 지정하였다.  
* 만약 사용자 정의 검증기가 폼 컨트롤 요소에 적용된다면 매개변수 타입을 FormControl로 지정하여도 된다.  
* 매개변수로 전달받은 검증 대상 폼 모델(위 예제의 경우, passwordGroup)에서 password와 confirmPassword을 취득하고 두 값을 비교한다.  
* 두 값이 불일치하는 경우, 에러 내용을 나타내는 에러 객체를 반환한다.  
* 이 에러 객체는 템플릿에서 userForm.controls.passwordGroup.errors?.match로 참조할 수 있다.  
* 두 값이 일치하여 오류가 발생하지 않는 경우, null을 반환한다. 이때 passwordGroup.errors는 null이 된다.  
* 사용자 정의 검증기는 빌트인 검증기와 동일한 방식으로 사용한다.

```javascript
import { PasswordValidator } from './password-validator';
...

ngOnInit() {
  this.userForm = new FormGroup({
    passwordGroup: new FormGroup({
      password: new FormControl('', Validators.required),
      confirmPassword: new FormControl('', Validators.required)
    }, PasswordValidator.match)
  });
}
```

## Formly
* https://formly-js.github.io/ngx-formly/  
* `ngx-formly`은 JavaScript / JSON으로 구성된 양식을 사용자 정의하고 렌더링하는 할 수 있는 Angular 모듈이다.  
* `formly-form` 컴포넌트와`FormlyConfig` 서비스는 입력 폼 컨트롤 개발 시 높은 유지 보수성을 제공한다.  
* 예제) https://run.stackblitz.com/api/angular/v1?file=src%2Fapp%2Fapp.component.ts  

```javascript
import { Component } from '@angular/core';
import { FormGroup } from '@angular/forms';
import { FormlyFormOptions, FormlyFieldConfig } from '@ngx-formly/core';

@Component({
  selector: 'formly-app-example',
  template: `
  <form [formGroup]="form" (ngSubmit)="submit()">
  <formly-form [model]="model" [fields]="fields" [options]="options" [form]="form">
    <button type="submit" class="btn btn-primary submit-button">Submit</button>
    <button type="button" class="btn btn-default" (click)="options.resetModel()">Reset</button>
  </formly-form>
</form>
`,
})
export class AppComponent {
  form = new FormGroup({});
  model: any = {};
  options: FormlyFormOptions = {
    formState: {
      awesomeIsForced: false,
    },
  };
  fields: FormlyFieldConfig[] = [
    {
      key: 'text',
      type: 'input',
      templateOptions: {
        label: 'Text',
        placeholder: 'Formly is terrific!',
        required: true,
      },
    },
    {
      key: 'nested.story',
      type: 'textarea',
      templateOptions: {
        label: 'Some sweet story',
        placeholder: 'It allows you to build and maintain your forms with the ease of JavaScript :-)',
        description: '',
      },
      expressionProperties: {
        'templateOptions.focus': 'formState.awesomeIsForced',
        'templateOptions.description': (model, formState) => {
          if (formState.awesomeIsForced) {
            return 'And look! This field magically got focus!';
          }
        },
      },
    },
    {
      key: 'awesome',
      type: 'checkbox',
      templateOptions: { label: '' },
      expressionProperties: {
        'templateOptions.disabled': 'formState.awesomeIsForced',
        'templateOptions.label': (model, formState) => {
          if (formState.awesomeIsForced) {
            return 'Too bad, formly is really awesome...';
          } else {
            return 'Is formly totally awesome? (uncheck this and see what happens)';
          }
        },
      },
    },
    {
      key: 'whyNot',
      type: 'textarea',
      expressionProperties: {
        'templateOptions.placeholder': (model, formState) => {
          if (formState.awesomeIsForced) {
            return 'Too bad... It really is awesome! Wasn\'t that cool?';
          } else {
            return 'Type in here... I dare you';
          }
        },
        'templateOptions.disabled': 'formState.awesomeIsForced',
      },
      hideExpression: 'model.awesome',
      templateOptions: {
        label: 'Why Not?',
        placeholder: 'Type in here... I dare you',
      },
    },
    {
      key: 'custom',
      type: 'custom',
      templateOptions: {
        label: 'Custom inlined',
      },
    },
  ];

  submit() {
    if (this.form.valid) {
      alert(JSON.stringify(this.model));
    }
  }
}
```

## Ngx Errors
* https://github.com/UltimateAngular/ngx-errors
* Reactive form 대한 유효성 검증 오류를 쉽게 구현할 수 있는 Angular 모듈이다.

```javascript
<!-- without ngxErrors -->
<input type="text" formControlName="foo">

<div *ngIf="form.get('foo').hasError('required') && form.get('foo').touched">
  Field is required
</div>
<div *ngIf="form.get('foo').hasError('minlength') && form.get('foo').dirty">
  Min length is 5
</div>
```

```javascript
<!-- with ngxErrors -->
<input type="text" formControlName="foo">

<div ngxErrors="foo">
  <div ngxError="required" when="touched">
    Field is required
  </div>
  <div ngxError="minlength" when="dirty">
    Min length is 5
  </div>
</div>
```
