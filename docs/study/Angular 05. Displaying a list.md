# 4. 영웅 목록 관리
이 페이지에서 프로그램을 확장하여 영웅 목록을 표시하고 사용자가 영웅을 선택하고 영웅의 세부 정보를 확인 할 수있게합니다.




## 모의 영웅 만들기
----------

프로그램에 표시 할 영웅이 필요합니다.

사실 원격 데이터 서버에서 가져올 수 있지만 지금 당장 당신은 모의 영웅을 만들어 서버에서 나온 척합니다.

mock-heroes.ts라는 파일을 src / app / 폴더에 만듭니다. HEROES 상수를 10명의 영웅 배열로 정의하고 내보내십시오. 파일은 다음과 같아야합니다.

src/app/mock-heroes.ts

    import { Hero } from './hero';
    
    export const HEROES: Hero[] = [
      { id: 11, name: 'Mr. Nice' },
      { id: 12, name: 'Narco' },
      { id: 13, name: 'Bombasto' },
      { id: 14, name: 'Celeritas' },
      { id: 15, name: 'Magneta' },
      { id: 16, name: 'RubberMan' },
      { id: 17, name: 'Dynama' },
      { id: 18, name: 'Dr IQ' },
      { id: 19, name: 'Magma' },
      { id: 20, name: 'Tornado' }
    ];



## 영웅 목록 전시
----------

영웅 목록을 HeroesComponent 맨 위에 표시하려고합니다.

HeroesComponent 클래스 파일을 열고 모의 HEROES를 가져옵니다.

src/app/heroes/heroes.component.ts (import HEROES)

    import { HEROES } from '../mock-heroes';


    heroes = HEROES;




## *ngFor로 영웅 목록 가져오기
----------

 HeroesComponent 템플릿 파일을 열고 다음과 같이 변경하십시오.

heroes.component.html (heroes template)

    <h2>My Heroes</h2>
    <ul class="heroes">
      <li>
        <span class="badge">{{hero.id}}</span> {{hero.name}}
      </li>
    </ul>

위의 영웅을 전시하는 템플릿을 아래의 템플릿으로 변경합니다.


    <li *ngFor="let hero of heroes">

ngFor는 Angular의 지시어입니다. 목록의 각 요소에 대해 호스트 요소를 반복합니다.
여기서 호스트 요소는 <li>입니다.

ngFor 앞에 별표 (*)를 잊지 마십시오. 구문의 중요한 부분입니다.




## 프로그램 Style
----------

영웅 목록은 매력적이어야하며 사용자가 마우스를 가져 가서 목록에서 영웅을 선택하면 시각적으로 반응해야합니다.

첫 번째 자습서에서는 styles.css에서 전체 응용 프로그램의 기본 스타일을 설정합니다. 그 스타일 시트는이 영웅 목록에 대한 스타일을 포함하지 않았습니다.

styles.css에 스타일을 추가하고 구성 요소를 추가 할 때 스타일 시트를 계속 확장 할 수 있습니다.

특정 구성 요소에 대해 비공개 스타일을 정의하고 구성 요소가 필요로하는 모든 것을 코드, HTML 및 CSS와 함께 한 곳에서 유지하는 것을 선호 할 수 있습니다.

이 방법을 사용하면 전역 스타일이 다른 경우에도 구성 요소를 다른 곳으로 재사용하고 구성 요소의 의도 된 모양을보다 쉽게 전달할 수 있습니다.

개인 스타일은 @ Component.styles 배열의 인라인 또는 @ Component.styleUrls 배열의 스타일 시트 파일로 정의합니다.

CLI가 HeroesComponent를 생성 할 때 HeroesComponent에 대한 빈 heroes.component.css 스타일 시트를 작성하고 이와 같이 @ Component.styleUrls에서 가리켰습니다.


src/app/heroes/heroes.component.ts (@Component)

    @Component({
      selector: 'app-heroes',
      templateUrl: './heroes.component.html',
      styleUrls: ['./heroes.component.css']
    })

heroes.component.css 파일을 열고 HeroesComponent의 개인 CSS 스타일을 붙여 넣습니다. 이 가이드 맨 마지막 코드 검토에서 찾을 수 있습니다.

@Component 메타 데이터에서 식별 된 스타일 및 스타일 시트는 해당 특정 구성 요소로 범위가 지정됩니다. heroes.component.css 스타일은 HeroesComponent에만 적용되며 다른 구성 요소의 외부 HTML 또는 HTML에는 영향을 미치지 않습니다.



## 마스터 / 세부 사항

사용자가 마스터 목록에서 영웅을 클릭하면 구성 요소는 선택한 영웅의 세부 정보를 페이지 하단에 표시해야합니다.

이 섹션에서는 주인공 아이템 클릭 이벤트를 듣고 영웅 세부 사항을 업데이트합니다.

**클릭 이벤트 바인딩**

heroes.component.html (template excerpt)

    <li *ngFor="let hero of heroes" (click)="onSelect(hero)">

이것은 Angular의 이벤트 바인딩 구문의 예입니다.
주위의 괄호는 요소의 클릭 이벤트를 앵귤러가 수신하기 위해 사용합니다. 사용자가 <li>을 클릭하면 Angular는 onSelect 함수를 실행합니다. onSelect 함수는 HeroesComponent의 메소드입니다. Angular는 * ngFor 표현식에서 이전에 정의된 것과 동일한 영웅 즉 클릭된 영웅을 호출합니다.



## 클릭 이벤트 핸들러 추가

컴포넌트의 hero 속성의 이름을 selectedHero로 변경하고 Hero 타입만 정해주고 초기화하지 않습니다. 응용 프로그램이 시작될 때 선택된 영웅은 없습니다.

다음 onSelect () 메서드를 추가합니다.이 메서드는 템플릿의 클릭 된 영웅을 구성 요소의 selectedHero에 할당합니다.

src/app/heroes/heroes.component.ts (onSelect)

    selectedHero: Hero;
    
    onSelect(hero: Hero): void {
      this.selectedHero = hero;
    }

템플리트는 더 이상 존재하지 않는 컴포넌트의 영웅 속성을 여전히 참조합니다. 영웅 속성의 이름을 selectedHero로 변경하십시오.

heroes.component.html (selected hero details)

    <h2>{{ selectedHero.name | uppercase }} Details</h2>
    <div><span>id: </span>{{selectedHero.id}}</div>
    <div>
      <label>name:
        <input [(ngModel)]="selectedHero.name" placeholder="name">
      </label>
    </div>



## *ngIf로 빈 정보창 숨기기
----------

브라우저가 새로 고쳐지면 응용 프로그램이 에러가 납니다.
브라우저 개발자 도구를 열고 콘솔에서 다음과 같은 오류 메시지를 찾습니다.


![](https://d2mxuefqeaa7sj.cloudfront.net/s_82D12E231D7C6D450F789E49C8D43925D704FBF3464B201F12D07C903AEE9376_1520949754455_image.png)


이제 목록 항목 중 하나를 클릭하십시오. 응용 프로그램이 다시 작동하는 것 같습니다. 영웅이 목록에 표시되고 클릭 된 영웅에 대한 세부 정보가 페이지 하단에 나타납니다.

**어떻게 된 거예요?**
앱이 시작되면 selectedHero가 의도적으로 정의되지 않습니다.

선택한 영웅이 없으므로 {{selectedHero.name}}과 (와) 같은 selectedHero 표현식의 속성을 참조하는 템플릿의 바인딩 표현식이 실패합니다.

수정 프로그램
구성 요소에는 선택한 영웅이있는 경우 선택한 영웅 세부 정보 만 표시되어야합니다.

영웅 세부 사항 HTML을 <div>로 묶습니다. Angular의 * ngIf 지시문을 <div>에 추가하고 selectedHero로 설정합니다.


    ngIf 앞에 별표 (*)를 잊지 마십시오. 구문의 중요한 부분입니다.


src/app/heroes/heroes.component.html (*ngIf)

    <div *ngIf="selectedHero">
    
      <h2>{{ selectedHero.name | uppercase }} Details</h2>
      <div><span>id: </span>{{selectedHero.id}}</div>
      <div>
        <label>name:
          <input [(ngModel)]="selectedHero.name" placeholder="name">
        </label>
      </div>
    
    </div>

브라우저가 새로 고쳐지면 이름 목록이 다시 나타납니다. 세부 정보 영역이 비어 있습니다. 영웅을 클릭하면 세부 정보가 나타납니다.

**왜 작동 하는가?**
selectedHero가 정의되지 않은 경우 ngIf는 DOM에서 영웅 디테일을 제거합니다. 걱정할 선택 영웅 바인딩이 없습니다.
사용자가 영웅을 선택하면 selectedHero에는 값이 있고 ngIf는 영웅 디테일을 DOM에 넣습니다.
선택한 영웅을 스타일링합니다.
모든 요소가 똑같이 보이면 목록에서 선택한 영웅을 식별하기가 어렵습니다.
사용자가 "Magneta"를 클릭하면 그 영웅은 다음과 같이 특유하지만 미묘한 배경색으로 렌더링해야합니다.


![](https://d2mxuefqeaa7sj.cloudfront.net/s_82D12E231D7C6D450F789E49C8D43925D704FBF3464B201F12D07C903AEE9376_1520949870830_image.png)


선택한 영웅 색칠은 이전에 추가 한 스타일의 .selected CSS 클래스의 작업입니다. .selected 클래스를 사용자가 클릭 할 때에 적용하면됩니다.
Angular 클래스 바인딩을 사용하면 CSS 클래스를 조건부로 쉽게 추가하고 제거 할 수 있습니다. 스타일을 지정하려는 요소에 [class.some-css-class] = "some-condition"을 추가하기 만하면됩니다.
HeroesComponent 템플릿의 <li>에 다음 [class.selected] 바인딩을 추가합니다.

heroes.component.html (toggle the 'selected' CSS class)

    [class.selected]="hero === selectedHero"

현재 행의 영웅이 selectedHero와 같을 때 Angular는 선택된 CSS 클래스를 추가합니다. 두 영웅이 다른 경우 Angular가 클래스를 삭제합니다. 완성된 <li>은 다음과 같습니다.

heroes.component.html (list item hero)

    <li *ngFor="let hero of heroes"
      [class.selected]="hero === selectedHero"
      (click)="onSelect(hero)">
      <span class="badge">{{hero.id}}</span> {{hero.name}}
    </li>




