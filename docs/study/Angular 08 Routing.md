# 라우팅(Routing)
> *라우트(route)란 한 곳에서 다른 곳으로 가기 위해 따라가는 길 혹은 경로를 의미한다.  
> Angular에서는 한 컴포넌트가 다른 컴포넌트로 이동하게 되는 경로를 명시하고 이에 맞게 컴포넌트가 이동하도록 한다.*  


##**순서**
* 라우터 모듈 생성
* 라우트 정의
* 라우터 아울렛을 통한 컴포넌트 전시
* 네비게이션 링크 생성 및 이동

## 라우팅 모듈(Routing Module) 생성
#### Angular CLI로 라우팅 모듈을 생성한다.
```bash
ng generate module app-routing --flat --module=app
```  
* flat 옵션은 src/app 경로에 모듈을 추가하도록 한다.
* module-app 옵션은 AppModule의 imports에 등록하도록 한다.  

#### 생성된 라우팅 모듈을 수정한다.
```javascript
import { NgModule }             from '@angular/core';
import { RouterModule, Routes } from '@angular/router';

@NgModule({
  exports: [ RouterModule ]
})
export class AppRoutingModule {}
```
* 자동으로 추가된 CommonModule은 제거한다.
* AppModule에서 RouterModule을 사용하기 위해 RouterModule을 exports에 추가한다.

## 라우트(routes) 정의
```javascript
import { HeroesComponent }      from './heroes/heroes.component';

const routes: Routes = [
  { path: 'heroes', component: HeroesComponent }
];
```
* path: 브라우저 주소에 표시되는 URL
* component: 해당 path에 접근했을 때 생성되어야 할 컴포넌트를 정의

```javascript
imports: [ RouterModule.forRoot(routes) ],
```
* 정의한 경로(routes)를 RouterModule의 루트에 추가한다.

## 라우터 아울렛(RouterOutlet) 추가
```javascript
<h1>{{title}}</h1>
<router-outlet></router-outlet>
<app-messages></app-messages>
```
* 라우터 아울렛은 라우트(routes)에 정의한 경로(path)에 접근하였을 때 해당 컴포넌트(component)를 전시한다.  

## 네비게이션 링크 생성 및 이동
#### 라우터 링크(routerLink)를 추가한다.
```javascript
<h1>{{title}}</h1>
<nav>
  <a routerLink="/heroes">Heroes</a>
</nav>
<router-outlet></router-outlet>
<app-messages></app-messages>
```
* routerLink는 명시한 경로로 이동할 수 있는 링크를 생성하는 속성이다.

#### 네비게이션 경로를 정의한다.
```javascript
{ path: '', redirectTo: '/dashboard', pathMatch: 'full' },
```
* pathMatch는 URL 경로가 완전 일치할 때 리다이랙션하도록 한다.  

```javascript
{ path: 'detail/:id', component: HeroDetailComponent },
```
* 파라미터가 포함된 URL일 경우에 ":id"와 같이 정의한다.  

```javascript
<a *ngFor="let hero of heroes" routerLink="/detail/{{hero.id}}">
```
* 인터폴레이션으로 id 파라미터 URL을 정의하면 해당 경로가 정해진다.  

#### 컴포넌트에서 네비게이션을 추가한다.
```javascript
getHero(): void {
  const id = +this.route.snapshot.paramMap.get('id');
  this.heroService.getHero(id)
    .subscribe(hero => this.hero = hero);
}
```
* ActivatedRoute의 route.snapshot.paramMap.get() 메소드를 통해 들어온 경로의 파라미터(id) 값을 가져올 수 있다.  

```javascript
this.router.navigate(['/heroes'])
```
* Router의 navigate() 메소드를 통해 경로를 이동할 수 있다.