# HTTP
> *Angular는 HTTP 통신을 위한 ajax wrapper 모듈을 제공한다. 또한 RxJs의 Observable을 반환하여 비동기 처리를 수려하게 할 수 있도록 한다.*  


##**순서**
* 라우터 모듈 생성
* 라우트 정의
* 라우터 아울렛을 통한 컴포넌트 전시
* 네비게이션 링크 생성 및 이동

## HttpClient 등록
#### HttpClientModule을 추가한다.
```bash
import { HttpClient } from '@angular/common/http';
```  
* Angular [4.3.0](https://github.com/angular/angular/blob/master/CHANGELOG.md#430-2017-07-14) 에 새롭게 추가된 HttpClientModule을 추가한다.

#### 서비스를 정의한다.
```javascript
getHeroes (): Observable<Hero[]> {
  return this.http.get<Hero[]>(this.heroesUrl)
}
```
* 반환 타입이 Observable<Hero[]>라는 것은 Hero 배열의 Observable 객체를 의미한다.
* HttpClient의 모든 반환 타입은 Observable이다.
* http의 get, post, delete, put등의 메소드를 이용한다.  

#### 에러를 핸들링한다.
```javascript
import { catchError, map, tap } from 'rxjs/operators';
```
* rxjs의 operator를 적절히 활용한다.  

```javascript
getHeroes (): Observable<Hero[]> {
  return this.http.get<Hero[]>(this.heroesUrl)
    .pipe(
      catchError(this.handleError('getHeroes', []))
    );
}```
* pipe()는 응답 결과를 확장한다.(pipe() 내부에 정의한 operator를 수행한다.)
* catchError()은 Observable의 실패 시에 인터셉터하는 operator이다.  

## HTTP 서비스 정의
#### hero 조회
```bash
getHero(id: number): Observable<Hero> {
  const url = `${this.heroesUrl}/${id}`;
  return this.http.get<Hero>(url).pipe(
    tap(_ => this.log(`fetched hero id=${id}`)),
    catchError(this.handleError<Hero>(`getHero id=${id}`))
  );
}
```  
* hero의 id를 통해 hero 객체를 가져온다. 
* tap oprator는 RxJs 5.5 부터 do로 키워드가 바뀌었다.
* do는 바이패스용 operator이다.

#### hero 업데이트
```javascript
updateHero (hero: Hero): Observable<any> {
  return this.http.put(this.heroesUrl, hero, httpOptions).pipe(
    tap(_ => this.log(`updated hero id=${hero.id}`)),
    catchError(this.handleError<any>('updateHero'))
  );
}
```
* 업데이트는 http.put() 메소드를 이용하였다.  

#### hero 등록
```javascript
addHero (hero: Hero): Observable<Hero> {
  return this.http.post<Hero>(this.heroesUrl, hero, httpOptions).pipe(
    tap((hero: Hero) => this.log(`added hero w/ id=${hero.id}`)),
    catchError(this.handleError<Hero>('addHero'))
  );
}
```
* 등록은 http.post() 메소드를 이용하였다.  

#### hero 삭제
```javascript
deleteHero (hero: Hero | number): Observable<Hero> {
  const id = typeof hero === 'number' ? hero : hero.id;
  const url = `${this.heroesUrl}/${id}`;

  return this.http.delete<Hero>(url, httpOptions).pipe(
    tap(_ => this.log(`deleted hero id=${id}`)),
    catchError(this.handleError<Hero>('deleteHero'))
  );
}

```
* "|" 인자를 or로 받아 처리한다.
* 삭제는 http.delete() 메소드를 이용하였다.  

## With RxJs
#### AsyncPipe을 통한 구독
```javascript
heroes$: Observable<Hero[]>;
```
* Observable 객체 타입의 heroes를 정의한다.  

```javascript
<li *ngFor="let hero of heroes$ | async" >
```
* '$'는 Observable 객체를 의미하는 관습이다.
* async라는 명명법의 AsyncPipe는 Observable을 자동으로 구독한다.  

#### Subject
```javascript
private searchTerms = new Subject<string>();

// Push a search term into the observable stream.
search(term: string): void {
  this.searchTerms.next(term);
  
this.heroes$ = this.searchTerms.pipe(
  // wait 300ms after each keystroke before considering the term
  debounceTime(300),

  // ignore new term if same as previous term
  distinctUntilChanged(),

  // switch to new search observable each time the term changes
  switchMap((term: string) => this.heroService.searchHeroes(term)),
);
```
* Subject는 Observable의 원천이며 Observable 그 자체이다.
* 따라서 Subject는 Observable로써 구독할 수 도 있다.
* next(value)를 통해 Observable에 value를 푸시할 수 도있다.
* debounceTime(300)은 300 밀리 초동안 새로운 이벤트를 기다린다. 과도한 HTTP 통신을 방지하는 방법 중에 하나이다.
* distinctUntilChaged()는 텍스트가 변경되는 경우에만 요청을 보낸다.
* switchMap()은 기존 Observable들을 파기하고 새로운 Observable을 생성하여 처리한다.