# 1. 튜토리얼 소개
Tour of Heroes 튜토리얼은 Angular의 기본 사항을 다룹니다.
이 튜토리얼에서는 인력 제공 기관이 영웅의 안정을 관리하는 데 도움이되는 앱을 작성합니다.

이 기본 앱에는 데이터 기반 애플리케이션에서 찾을 수있는 많은 기능이 있습니다. 그것은 영웅의 목록을 획득하고 표시하며, 영웅의 세부 사항을 편집하고 영웅 데이터를 여러가지 관점으로 탐색해봅니다.

튜토리얼이 끝나면 다음을 수행 할 수 있습니다.


- 내장된 Angular 지시어를 사용하여 요소를 표시하거나 숨기고 영웅 데이터 목록을 표시합니다.
- 영웅의 세부 사항을 표시하고 영웅의 배열을 표시하려면 각도 구성 요소를 만드십시오.
- 읽기 전용 데이터에 단방향 데이터 바인딩을 사용하십시오.
- 편집 가능한 필드를 추가하여 양방향 데이터 바인딩으로 모델을 업데이트하십시오.
- 키 입력 및 클릭과 같은 사용자 이벤트에 구성 요소 메서드를 바인딩합니다.
- 사용자가 마스터 목록에서 영웅을 선택하고 세부보기에서 해당 영웅을 편집 할 수 있습니다.
- 파이프로 데이터를 포맷하십시오.
- 영웅을 모으는 공유 서비스를 만듭니다.
- 라우팅을 사용하여 다양한보기와 해당 구성 요소를 탐색합니다.
- Angular가 시작할 때 자신이 필요로하는 것을 무엇이든 할 수 있다는 자신감을 얻으려면 Angular를 배우십시오.

모든 튜토리얼 단계를 완료 한 후 최종 앱은이 라이브 예제 / 다운로드 예제([live example](https://angular.io/generated/live-examples/toh-pt6/stackblitz.html) / [download example](https://angular.io/generated/zips/toh-pt6/toh-pt6.zip))처럼 보입니다.





## 만들어볼 앱

다음은 "대시 보드" 입니다.

![Output of heroes dashboard](https://angular.io/generated/images/guide/toh/heroes-dashboard-1.png)


대시 보드 위의 두 링크 ( '대시 보드'및 '영웅')를 클릭하여 이 대시 보드 보기와 영웅보기를 탐색 할 수 있습니다.

대시 보드 영웅 "Magneta"를 클릭하면 라우터가 영웅의 이름을 변경할 수있는 "영웅 세부 정보"를 엽니다.

![Details of hero in app](https://angular.io/generated/images/guide/toh/hero-details-1.png)


"뒤로"버튼을 클릭하면 대시 보드로 돌아갑니다. 상단의 링크는 주요 보기를 안내합니다. '영웅'을 클릭하면 앱에 '영웅' 목록이 표시됩니다.

![Output of heroes list app](https://angular.io/generated/images/guide/toh/heroes-list-2.png)


다른 영웅 이름을 클릭하면 목록 아래의 읽기 전용 미니 세부 사항이 새로운 선택 사항을 반영합니다.

"세부 정보보기"버튼을 클릭하면 선택한 영웅의 편집 가능한 세부 정보를 볼 수 있습니다.

다음 다이어그램은 모든 탐색 옵션을 캡처합니다.


![View navigations](https://angular.io/generated/images/guide/toh/nav-diagram.png)



![Tour of Heroes in Action](https://angular.io/generated/images/guide/toh/toh-anim.gif)






