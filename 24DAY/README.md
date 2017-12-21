# DAY24 12.14 
 ## 트랜스 파일러 Babel (코드 변환기) 
 - .js : 트랜스파일러 거치기 전 파일. 여러파일들이 es2051모듈이란 이름으로 연결되어있다.
 - Snake Game - > .js : babel 을 거처서 나오게 설계되어있다.
 - 웹사이트 만들때 파일수가 적으면 좋다.
 - 많은 파일들을 어떻게 웹상에서 사용자에게 제공 할것인가?
 ## webpack: 모듈 번들러
 - 수많을 파일들을 하나로 묶어준다.
 - 웹브라우저가 해석 할 수있는 언어로 변환
 - 모듈 번들러를 잘못쓰면 js, css 디버깅 하기 어려워진다. -> 소스맵(sourcemap)
    - 웹팩이 파일을 만들어 낼때 bundle.js.map (각각의 라인이 어디에서 유례했는지 기록)
    - 번들러를 거치기 전 과 후의 관계를 기록한다.
    - 인스팩터에서 소스맵을 확인할수 있다.
    - Snake Game (webpack/development.js -> devtool: 소스맵 활성)
 - 번들러의 세대교체
  - webpack은 느리다. (최신버전의 자바스크립트기술을 활용 못함)
  - 차세대 번들러 
    - rollup
    - fusebox
    - brunch
    - **parcel** (소스맵과같은 기능은 없다.) !! 기억해 둘것
 
  - 비쥬얼 스튜디오 코드 도구
    - .editorconfig : 에디터가 설정된 값으로 실행된다. 가이드라인.(editorconfig 설치해야 적용됨.)
    - 사용하는 에디터마다 기본설정이 다르기 때문에 같은 가이드라인을 설정한다.
    - **Debugger : chromedebugger 확장 프로그램 설치 -> Ctrl+Shift+P (cmd +Shift+ P ) 디버그: launch.json열기  -> chrome 선택**
      - 빨간점 찍기(중단점) : js가 실행 되다가 중단점에서 멈춤.
## snake-game project
```js
SnakeGameLogic.prototype.up = function () {
  console.log('up');
}
SnakeGameLogic.prototype.down = function () {
  console.log('down');
}
SnakeGameLogic.prototype.left = function () {
  console.log('left');
}
SnakeGameLogic.prototype.right = function () {
  console.log('right');
}
SnakeGameLogic.prototype.nextState = function () {
  
  console.log(`nextState`);
  return true;
}
```
```js
SnakeGameLogic.prototype = {
    up() {
        // 위쪽 화살표 키를 누르면 실행되는 함수
        console.log('up');
    },
    down() {
        // 아래쪽 화살표 키를 누르면 실행되는 함수
        console.log('down');
    },
    left() {
        // 왼쪽 화살표 키를 누르면 실행되는 함수
        console.log('left');
    },
    right() {
        // 오른쪽 화살표 키를 누르면 실행되는 함수
        console.log('right');
    },
    nextState() {
        // 한 번 움직여야 할 타이밍마다 실행되는 함수
        // 게임이 아직 끝나지 않았으면 `true`를 반환
        // 게임이 끝났으면 `false`를 반환
        console.log(`nextState`);
        return true;
    },
}
```
- **프로토타입 밑에 각각의 메소드를 추가하는 방식은 constructor가 지워진다. 하지만 수정에 용이하다.**

### 뱀 움직이게 만들기
```js
SnakeGameLogic.prototype.nextState = function () {

   for (let c of this.joints) {
    c.x ++;
    // c.x += 1;
    //c['x'] += 1;
  }

  console.log(`nextState`);
  return true;
}
```
### vs code
- command + enter : 문장중간에 **하단**으로 줄바꾸기
- command +shift +enter : 문장중간에 **상단**으로 줄바꾸기
----
### 배열
1.배열생성하기
```js
const number = [ ]
new Array(1)
Array.of(1,2,3) //정적메소드 사용
Array.from('hello')
new Array(10).fill(1) 
```

2.요소 읽기
- 인덱스를 사용한다.(0 이상의 정수)
- fill 메소드
```js
arr.fill(0);
```

3.배열의 시작/끝부분에서 요소를 추가/제거하기
```js
arr.pop(); //끝부분 삭제
arr.push(); //끝부분 추가
arr.shift(); //시작 삭제
arr.unshift(); //시작 추가
```

4.배열 중간에 삽입하기
- splice 범용으로 쓰임
```js
[1,2,3,4,5]
// 배열의 연속된 요소들을 다른 요소 추가하거나 삭제할때
let arr = [1,2,3,4,5];
arr.splice(1,3,'two','three','four'); //[2,3,4]
// 3개를 하나로 바꿀수도있다. 제한이 없다.
// splice(1,3) : 인덱스1부터 인덱스 포함 1,2,3까지.
```

5.배열 뒤집기
- reverse
- 원본을 통째로 뒤바뀐다.

6.배열 정렬하기
- 원본을 바꾼다.
- 메소드 인자에는 비교함수를 넣어줘야한다.
- 비교함수 : 기준을 설명해준다.
- compare(a,b) 
- arr.sort((x, y) => x - y)
- x - y 오름차순 , y - x 내림차순.
- 숫자가 뿐만아니라 어떤값이든 비교 할 수 있다.
  - 문자열길이 기준
- sort 함수에서는 무조건 비교함수가 있어야 한다.

7.배열이 특정 조건을 만족하는지 판별하기
- includes
- every : 조건중을 모두 만족해야 ture , AND
```js
const arr = ['one', 'two', 'three'];
arr.every(item => item.length > 2); // true 모든 요소가 조건에 만족하면 true
```
- some :  조건중이 하나라도 만족하면 true . OR
```js
const arr = ['one', 'two', 'three'];
arr.some(item => item.length > 2)
```
- predicate 
```js
//진리값을 반환하는 함수
function greaterThan2 (x){
  return x > 2;
}
// 화사표 함수 사용
const greaterThan3 = x => x > 3
const greaterThan3 = x => {return x > 3;}
```