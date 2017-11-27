# Orientation

* 박성백 강사님 메일 (sungback@naver.com) 블로그 (http://sungback.blog.me)
* 유망한 개발 언어
  * JavaScript
  * Python : 머신러닝 분야
  * Scala : 빅데이터 분야
* 프론트엔드 개발 언어(React.js, Angular, Vue.js) 중 React.js 에 집중
  * Angular는 Framework
  * React.js, Vue.js는 Library로 이러한 라이브러리를 적절히 조합해서 사용하는 것을 추천함
* 정확한 타겟을 잡고 공부를 하는 것이 중요 만들고 싶은 사이트를 목표로 삼아 배운 것들을 활용할 수 있는지 고민해볼 것

------

# Computational Thinking

## 컴퓨터의 발전 과정

* 에니악: 1946년 전자식 계산기 개발
* 트랜지스터의 개발 이후에 컴퓨터가 급격한 발전을 이루게 된다.
* 서버 운영체제 세계 점유율은 Linux가 96% 이상을 차지한다.
* 전 세계 프로그램 언어는 Unix -> Linux 로 발전해 왔다.
* 개인운영체제는 Unix -> DOS -> Windows 로 발전해 왔다.
* Free BSD -> MAC
* Unix의 유료화로 Linux를 개발하게 되면서 범용되게 되었다.
* Android, iOS 모두 Linux를 기반으로 만들어졌다.
* Git 역시 Linux가 개발함. Linux 버전 관리를 위해 개발됨.
* React의 핵심
  1. Component
  2. Virtual DOM : 메모리 상에 DOM의 상태를 유지하며 달라진 부분만을 DOM에 반영하여 DOM의 속도 문제를 해결
  3. 단방향 데이터 흐름
* 클라우딩 컴퓨팅: 사용자가 자신의 컴퓨터에 저장해둔 자료와 소프트웨어를 중앙 시스템인 대형 컴퓨터에 저장해두고, 원격으로 인터넷으로 접속하여 저장한 데이터에  접근하는 방법. ex. iCloud, Drive, N드라이브

------

## Web

- JavaScript 표준은 EcmaScript

- Babel로 ES6 개발버전을 ES5로 변환(IE 하위 버전 사용)할 수 있다.

- Chrome, Safari, Opera 등의 Browser는 사용자가 따로 업데이트 하지 않아도 JavaScript의 새로운 버전을 사용하고 있다(Evergreen). 

- OOP(Object Oriented Programming)의 Multi Thread 의 안정성 이슈로 인해 FP(Functional Programming) 로 비중이 이동하고 있다.

- Single Thread & Multi Thread

  - Single Thread: 프로세스에 하나의 제어 모델이 있는 것.
  - Multi Thread: 프로세스가 다수의 제어 스레드를 가지는 것으로 스레드 관리에는 효율적이지만 스레드가 긴 작업을 실행 할 경우 나머지 작업들은 대기하게 되는 문제가 있다. 
  - Node.js는 Non-blocking I/O와 단일 스레드 이벤트 루프를 통한 높은 처리 성능을 가지고 있다

- GUI(Graphic User Interface) 구현이 용이하여 OOP가 상대적으로 더 발전하게 됨.

- Javascript는 OOP와 FP 로 활용할 수 있지만 FP지향적이어야 한다.

- Moore's Law :1965년 고든 무어가 제시한 반도체의 집적회로의 성능이 24개월마다 2배로 증가한다는 법칙으로 현재에는 이러한 법칙이 무의미하게 되어 점차 싱글 스레드, FP 를 지향할 필요가 있다.

- 프로그램의 **응답시간**이 중요하기 때문에 Async(비동기) 방식을 사용한다. Non-blocking의 장점이 있다.

- async 방식 프로그램은 콜백이 복잡해지면서 내부에서 지속적으로 콜백을 사용하여 코드 읽기가 어려워지는 상태인 **콜백헬(Callback Hell)**이 발생 할 수 있다. Node.js에서는 이러한 콜백헬을 피하기 위해 async라이브러리가 존재한다.

- 대표적 status code: 200(Success), 404(Not Found), 500(Error)

- 백틱(Backtick) : ` 문자를 사용하는 ES6 템플릿 문자열로 JavaScript에 간단한 [문자열 채워넣기 (string interpolation)](https://en.wikipedia.org/wiki/String_interpolation) 기능이 가능하다.

  ```
  console.log("Server running at http://"+hostname+":"+port);

  console.log(`Server running at http://${hostname}:${port}/`); //ES6 style 
  ```


- 서버 사이드 렌더링을 통해서 사이트나 페이지에 대한 내용이 있어야 검색엔진에서 활용하여 검색 결과를 보여줄 수 있다.

- MVC Pattern

  |           | Model_데이터 | View_화면  | Controller_처리            |
  | --------- | --------- | -------- | ------------------------ |
  | Front-end | HTML      | CSS      | JS                       |
  | Back-end  | DataBase  | Template | DB와 Template의 요청 및 응답 처리 |

------

## Node.js

* NVM : Node Version Manager

  * mac: brew install nvm

  * windows: nvm-setup.zip (https://github.com/coreybutler/nvm-windows/releases/download/1.1.6/nvm-setup.zip) 다운로드 후 Windows PowerShell 실행

    * nvm install을 위한 명령어

       > nvm install 8.9.1

    * nvm 사용을 위한 명령어

       > nvm use 8.9.1

  * work 디렉토리 생성

    ```
     mkdir work
    ```

  * work 디렉토리 하위에 server.js 생성

    ```
    const http = require('http');
    const hostname = '127.0.0.1'; //localhost 내 컴퓨터
    const port = 3000; //web-server port는 80 

    const server = http.createServer((req, res) => {
      res.statusCode = 200;
      res.setHeader('Content-Type', 'text/plain');
      res.end('Hello World\n');
    });

    server.listen(port, hostname, () => {
      console.log(`Server running at http://${hostname}:${port}/`);
    });

    ```

    * (req, res) 입력 => {} 출력, 실행

  * server.js 실행

    ```
    node server.js
    ```

  * nodemon 모듈(서버 변화를 실시간으로 반영해주는 모듈) 설치

    ```
    npm install -g nodemon
    ```

  * nodemon으로 서버 실행

    ```
    nodemon server.js
    ```

  * express-generator 모듈 설치

    ```
    npm i -g express-generator
    ```

  * express 활용하여 'exp1' 프로젝트의 기본 틀을 생성

    ```
    express --ejs exp1
    ```

  * server 실행

    ```
    npm start
    ```


------

## ETC

* 코딩, 소프트웨어 시대 - 직업의 미래 (https://www.youtube.com/watch?v=jiqOZdcJXN4)
* data-scientist : 수학, 통계분야를 통해서, 소프트웨어엔지니어를 통해서 
* DeBug(디버그)를 통해서 버그를 없앤다.
* Node.js / git / Amazon web service 를 이용한 실습 위주의 수업을 진행한다.
* 참고서적

  *  **러닝 자바스크립트 ES6로 제대로 입문하는 모던 자바스크립트 웹 개발** (이선 브라운 저 / 한선용 역 | 한빛미디어)

  *  **Do it! Node.js 프로그래밍** (정재곤 저 | 이지스퍼블리싱)

  *  **자바스크립트와 Node.js를 이용한 웹 크롤링 테크닉** (쿠지라 히코우즈쿠에 저 / 이동규 역 | 제이펍)

  *  **Node.js 6.x 블루프린트** (페르난두 몬테이루 저 / 맹기완, 임보은 공역 | 한빛미디어)
