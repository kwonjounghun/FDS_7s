## 큐, 스택, 트리
- 데이터의 추상적 형태와 그 데이터를 다루는 방법.
### 큐
- 파이프라고 생각
- 선형 자료형
- FIFO(선입선출)
- enqueue,dequeue 작업을 할수 있어야 큐이다.
- 순서대로 처리해야하는 작업을 임시로 저장해두는 버퍼로 사용.
- ex)유투브 
###스택
- 통이라고 생각
- 선형자료형
- LIFO  (후입선출)
- push.pop.peak(맨나중의 데이터 확인)
- 여러작업을 수행하면서 이전의 작업 내용을 저장해 둘 필요가 있을때
- ex)control + z, ctr+y(스택을 하나더 만들어서 ctr+z 한 내용을 넣으는 구조) 
### 트리

##비동기 프로그래밍
    - 프로그래밍 기법 : 어떤 작업이 오래걸릴때(ex: fetch('google.com') 시간이 오래걸려(1~5초) 그동안 다른작업을 할수 있게 해준다.)
##Motivation - 타이머 API
- setTimeout() : 일정시간 후에
- setInterVal() : 일정시간 마다
- UI와 관련되서 쓰게 되는 경우가 많다.
- debounce (입력폼에서 입력하고있는중에 이미사용중인 아이디입니다.) : 손을 놓고 일정시간 기다리면 실행. 1s간격보다 작은 간격으로 입력하면 진행 되지않고 1s보다 큰간격으로 입력하면 진행된다.
- throttle(키보드입력할때) : 시간간격이하로는 함수가 실행이 안되도록. 계속실행될때도 시간간격이하로는 실행이 안된다.
- npm 라이브러리
```js
function delay(cb, time) {
  return function() {
    setTimeout(cb, time);
  }
}

function debounce(cb, time) {
  let timeoutId;
  return function() {
    if (timeoutId) {
      clearTimeout(timeoutId);
    }
    timeoutId = setTimeout(() => {
      cb();
      timeoutId = null;
    }, time)
  }
}

function throttle(cb, time) {
  let throttled = false;
  let timeoutId;
  return function() {
    if (!timeoutId) {
      timeoutId = setTimeout(() => {
        throttled = false;
        timeoutId = null;
      }, time);
    }
    if (!throttled) {
      cb();
    }
    throttled = true;
  }
}
```
## 브라우저의 코드 실행 과정
### 호출 스택
- 스택형태의 저장소. 함수 호출과 관련된 정보를 관리
- 실행맥락 : 함수내부에서 사용되는 변수, 스코프체인, this가 가리키는 객체.
- debugger; -> 호출스택 확인하기
### 작업큐
- 기다려야되는일을 브라우져에 넘긴다
- 그결과와 콜백을 작업큐에 추가된다.
- 호출스택이 비어있으면 작업큐에서 꺼내와서 콜백을 실행한다.
- 이과정을 이벤트 루프라고한다.
- 먼저 위임된 콜백이 먼저 큐에 쌓이는것이 아니다.
- 작업큐에 등록된 순서대로 실행된다.
- 호출스택이 비어있는 순간에 화면을 그리는것이다. (호출스택만 비어있으면 브라우저는 화면을 그린다.)

## 비동기 프로그래밍(Asyncronouse Programing)
- 자바스크립트는 브라우져에 큐가 내장되어있다.
- 자바스크립트는 비동기 프로그래밍을 하기 최적화되어있다.


## github - issue(할일목록)

### promise
- 언젠가 끝나는 작을의 결과값을 담는 통.
- 만드는 시점에는 그통안에 무었이 들어갈지 모르수 있다.
- 값이 들어오는 순간 실행될 콜백을 미리 등록해둘수 있다.(then)
- 값이 채워지기 전에 then을 통해 콜백을 등록할 수 있다.
```js
const p = new Promise((resolve, reject) => {
  setTimeout(() => {
    console.log('2초가 지났습니다.'); 
    resolve('hello');
  }, 2000);
});
p.then(value => console.log(value)) // 2초가 지나기 전에 미리 등록해둔 콜백
```
```js
const p2 = p.then(msg => {
  return msg + ' world'; //새로운 promise가 만들어지고 p2 에 새로운 반환값이 들어간다.
});

p2.then(msg => {
  console.log(msg); // hello world
});


const p = new Promise((resolve, reject) => {
  setTimeout(() => {
    console.log('2초가 지났습니다.');
    resolve('hello');
  }, 2000);
});
p.then(msg => {
  return msg + ' world';
}).then(msg => {
  console.log(msg);
});

```
---
`.then().then()`
 
- Task Queue와 호출스택 사이에 중간 작업점이 존재
- 작업큐와 마이크로 작업큐가 있음
- 프로미스는 별도의 큐가 존재함(마이크로작업큐)
- 마이크로작업큐가 작업큐보다 먼저 실행되므로 동기식처럼 보이나
- 엄밀히 따지면 각각 다른 작업큐를 사용하므로 비동기방식
- then은 새로운 프로미스를 반환
