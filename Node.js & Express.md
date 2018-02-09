# Node.js
> 구글 크롬의 자바스크립트 엔진 (V8 Engine) 에 기반해 만들어진 서버 사이드 플랫폼이다.  
> 자바스크립트가 서버 사이드에서도 사용할 수 있게되어 자바스크립트의 입지를 넓힌 장본인이다.  
> 이벤트 기반, 논 블로킹 I/O 모델을 사용해 가볍고 효율적이다.
## 1. Node.js는 웹서버?
그렇지 않다. Node.js 자체로는 아무것도 하지 않는다.  
일부 라이브러리의 도움을 받아 HTTP 서버를 직접 작성해야한다.  
Node.js는 그저 코드를 실행할 수 있는 하나의 방법에 불과한 Javascript 런타임일 뿐이다.
## 2. 비동기 I/O 처리
Node.js 라이브러리의 모든 API는 비동기식이다. 네트워크 처리를 하거나 파일 I/O와 같은 일을 수행할 때 멈추지 않는다.(Non-Blocking)   
Node.js 기반 서버는 API가 실행되었을 때 데이터를 반환할 때까지 기다리지 않고 다음 API를 실행한다. 그리고 이전에 실행했던 API가 결과 값을 반환 할 시,  Node.js의 이벤트 알림 메커니즘을 통해 결과 값을 받아온다.  
## 3. 빠른 속도
구글 크롬의 V8 자바스크립트 엔진을 사용하여 빠르게 코드를 실행할 수 있다.
## 4. 단일 쓰레드 / 뛰어난 확장성
Node.js는 이벤트 루프와 함께 단일 쓰레드 모델을 사용하며, 이벤트 메커니즘은 서버가 멈추지않고 반응하도록 해주어 서버의 확장성을 키워준다.  
반면, 일반적인 웹서버는 (Apache) 요청을 처리하기 위하여 제한된 쓰레드를 생성한다.   
Node.js는 쓰레드를 한 개만 사용하고 Apache 같은 웹서버보다 훨씬 많은 요청을 처리할 수 있다.
## 5. 이럴 때 적용해라
 - 입출력이 잦은 어플리케이션
 - 데이터 스트리밍 어플리케이션
 - 데이터를 실시간으로 다루는 어플리케이션
 - JSON API 기반 어플리케이션
 - 싱글페이지 어플리케이션
## 6. 이럴 땐 쓰지마라
- 단일 쓰레드기반 환경이기 때문에 CPU 사용률이 높은 어플리케이션에서는 권장하지 않는다.
# NPM
> NodeSearch에서 탐색 가능한 Node.js 패키지/모듈 저장소  
> Node.js 패키지 설치 및 버전/호환성을 관리 할 수 있는 커맨드라인 유틸리티
## Package.json
노드 어플리케이션/모듈의 경로에 위치하며 패키지의 속성을 정의한다.
express로 프로젝트를 생성했을 때 생성되는 package.json 예시 (참고: http://programmingsummaries.tistory.com/385)
```json
{
  "name": "myapp",
  "version": "0.0.0",
  "private": true,
  "scripts": {
    "start": "node ./bin/www"
  },
  "dependencies": {
    "body-parser": "~1.13.2",
    "cookie-parser": "~1.3.5",
    "debug": "~2.2.0",
    "express": "~4.13.1",
    "jade": "~1.11.0",
    "morgan": "~1.6.1",
    "serve-favicon": "~2.3.0"
  }
}
```
## 모듈 관리
 - 모듈 조회: 다음 명령어로 모듈을 검색할 수 있다.
 ```{r, engine='bash', count_lines}
npm search [MODULE NAME]
```
 - 모듈 설치: 다음 명령어로 모듈을 설치할 수 있다.
 ```{r, engine='bash', count_lines}
npm install [MODULE NAME]
```
 - 모듈 제거: 다음 명령어로 설치된 모듈을 제거할 수 있다.
```{r, engine='bash', count_lines}
npm uninstall [MODULE NAME]
```

