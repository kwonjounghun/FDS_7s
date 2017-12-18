# javascript intensive #1

강사님 Javascript 교재에 요약이 잘 되어있기 때문에

수업 때 강조하셨던 부분이나 교재에 없는 추가 설명만 기재하였습니다.

참고 부탁 드립니다.

## let, const 변수와 블록 스코프

|       | ```const``` | ```let``` | ```var``` |
| ----- | ----------- | --------- | --------- |
| 스코프   | 블록 스코프      | 블록 스코프    | 함수 스코프    |
| 재대입   | X           | O         | O         |
| 재선언   | X           | X         | O         |
| 호이스팅  | X           | X         | O         |
| 사용 권장 | 1순위         | 2순위       | 3순위       |

## 전역 변수 (Global Variable)

전역 스코프는 스코프 체인의 가장 바깥쪽에 있는 스코프입니다.	

전역 스코프에서 선언된 변수를 **전역 변수(global variable)**라고 합니다.

변수를 명시적으로 전역 스코프에서 선언하지 않더라도, 한 번도 선언되지 않은 이름으로 안쪽 스코프에서 **let, const, var를 붙여주지 않고 변수를 선언**하면 전역 스코프에 변수가 만들어집니다.

```javascript
function func() {
  variable = 1; // `variable`이라는 변수가 선언된 적 없으므로, 전역 변수가 됩니다.
}

func();
console.log(variable); // 1
```

cf)HTML에서 <script src=""> 이렇게 쓰는 경우에만 전역 변수를 활용할 수 있고 활용시 주의해야 합니다. 중복된 변수의 재정의, 재대입 등으로 코드가 꼬일 수 있습니다.

webpack, parcel등 bundler를 활용하면 쓸 일이 없다고 하네요.

cf) 결합(coupling)보다는 응집(cohesive)이 잘 되어있는 코드가 좋은 코드라고 합니다.

전역변수가 등장하지 않도록 모듈화를 잘 해놓으면 오류를 만날 일이 줄어듭니다.



## 전역 객체(Global Object)

JavaScript 구동 환경은 모두 **전역 객체(Global Object)**라는 특별한 객체를 갖고 있습니다. 

```javascript
let foo = 1;
window.foo; // 1
```

| 구동 환경   | 전역 객체 이름 |
| ------- | -------- |
| 웹 브라우저  | `window` |
| 웹 워커    | `self`   |
| Node.js | `global` |

## 참조(Reference)

**참조(reference)**란, **객체가 컴퓨터 메모리 상에서 어디에 저장되었는 지를 가리키는 값**입니다.

### 함수호출

함수 호출 시에 객체를 인자로 넘긴다면, 이 때  **실제로 복사되는 것은 객체 자체가 아니라 참조**입니다. 참조를 이용해 **원본 객체의 내용을 변경할 수 있습니다.** 원본이나, 복사된 참조나 **같은 객체를 가리키기 때문입니다.**

```javascript
const obj = {};

function addProp(o) {
  o.prop = 1;
}

// 변수 `obj`에 저장되어 있는 참조가 매개변수 `o`에 복사됩니다.
addProp(obj);

console.log(obj.prop); // 1
```

## 객체의 같음

등호 연산자 역시, 객체의 내용을 비교하는 것이 아니라 **객체의 참조를 비교합니다.** 

```
{prop: 1} === {prop: 1}; // false
[1, 2, 3] === [1, 2, 3]; // false

```



## 불변성(Immutability)

원시 타입의 값 자체의 내용을 변경할 수 있는 방법은 **없습니다.** 이런 성질을 **불변성(immutability)**이라고 하고, "JavaScript의 원시 값은 불변(immutable)이다"라고 말합니다.

### 객체의 가변성

원시타입의 메소드는 모두 **기존 값을 바꾸는 것이 아니라 새로운 값을 반환합니다.**객체는 **가변(mutable)**입니다. 이 때문에 많은 줄에 코드를 작성시에는 이러한 특성이 프로그래밍에 어려움을 끼칩니다.

이럴때 객체의 가변성을 불변으로 바꿔주는 방법이 2가지 있습니다.

1) `Object.freeze`는 객체를 **얼려서** 속성의 추가/변경/삭제를 막습니다.

```javascript
const obj = {prop: 1};

Object.freeze(obj);

// 모두 무시됩니다.
obj.prop = 2;
obj.newProp = 3;
delete obj.prop;

console.log(obj); // { prop: 1 }
```

2) [Immutable.js](https://facebook.github.io/immutable-js/) 같은 라이브러리를 활용할 수 있습니다. 왼쪽의 라이브러리는 메소드를 통해 내용이 조금이라도 변경되면 아예 새로운 객체를 반환합니다. 즉, **내용이 달라지면 참조 역시 달라지게 되어** 객체의 내용이 변경되었는지를 확인하는 작업이 아주 쉬워집니다.

## 객체로서의 함수

함수 객체는 두 가지의 속성을 갖는다.

1. ```length``` - 매개변수의 갯수
2. ```name``` - 함수의 이름

```js
function sum(x, y, z) {
    return x + y + z;
}
console.log(sum.length); //3
console.log(add.name); // sum
```

## ```this``` 바꾸기

this를 원하는 값을 가리키게 만들 수도 있다.
```bind```,
```call```,
```apply```

### 1. ```bind```를 사용한 예제

```js
function printGrade(grade) {
    console.log(`#{this.name} 님의 점수는 ${grade}점 이다.`);
}
const student = {name: 'Mary'};
const printGradeForMary = printGarde.bind(student);
//위 코드에서 printgarde에서 사용하는 this가
//메소드로 넘겨준 인자 값인 student의 this를 가리키는 함수를 반환한다.

printGradeForMary(100); //Mary 님의 점수는 100점 이다.
// printGradeForMary(100)의 인자 100은 printGrade(grade)의 매개변수 grade이다.
```

### 2. ```call```을 사용한 예제

```js
function printGrade(grade) {
    console.log(`${this.name} 님의 점수는 ${grade}점 이다.`);
}
const student = {name: 'Mary'};

printGrade.call(student, 100);//Mary 님의 점수는 100점 이다.


function printGrade2(grade) {
    console.log(`${this.name} 님의 점수는 ${grade}점 이다.`);
}

printGrade2.call({name: 'Mary'}, 100);//Mary 님의 점수는 100점 이다.
//printGrade2.call의 인자에 직접 객체 형태로 전달해도 무방하다.
```

### 3. ```apply```를 사용한 예제 (```call```과 기능은 같지만 배열로 전달한다.)

```js
function printGrade(grade) {
    console.log(`${this.name} 님의 점수는 ${grade}점 이다.`);
}
const student = {name: 'Mary'};

printGrade.apply(student, [100]);//Mary 님의 점수는 100점 이다.


function printGrade2(grade) {
    console.log(`${this.name} 님의 점수는 ${grade}점 이다.`);
}

printGrade2.apply({name: 'Mary'}, [100]);//Mary 님의 점수는 100점 이다.
//printGrade2.apply 인자에 직접 객체 형태로 전달해도 무방하다.
```

## ```arguments```와 ```Rest Parameters```

```function``` 구문을 통해 생성된 함수가 호출될 때 ```arguments```라는 변수가 함수 내부에 자동으로 생성된다.
```arguments```는 *유사 배열 객체(array-like object)이자 *반복 가능한 객체(iterable object)이다.
함수에 인자가 순서대로 저장되어 인덱스를 가지고 인자를 읽거나
```for...of```로 순회할 수 있다.

### 1. ```arguments```를 사용하여 배열처럼 사용한 예제

```js
function sum(x, y, z) {
  console.log(arguments[0], arguments[1], arguments[2]); //1, 2, 3
  return x + y + z;
}

sum(1, 2, 3); // 6
```

### 2. ```for...of```와 ```reduce```를 사용한 예제

```js
function sum(...ns) {
  let result = 0;
  for (let item of ns) {
    result += item;
  }
  return result;
}

sum(1, 2, 3, 4); // 10


function sum2(...ns) {
  // `for...of` 루프 대신에 `reduce` 메소드를 사용해서 합계를 구할 수 있습니다.
  return ns.reduce((acc, item) => acc + item, 0);
}

sum2(1, 2, 3, 4); // 10
```

### 3. ```...```를 사용하여 모든 인자를 해당 매개변수에 저장하는 예제

```js
function printGrades(name, ...grades) {
  console.log(`${name} 학생의 점수는 ${grades.join(', ')} 입니다.`);
}

printGrades('Mary', 96, 78, 68); // Mary 학생의 점수는 96, 78, 68 입니다.
```



## 트리구조

트리(tree)는 여러 데이터가 **계층 구조** 안에서 서로 연결된 형태를 나타낼 때 사용됩니다.

![Tree](./capture.PNG)

트리를 다룰 때 사용되는 몇 가지 용어를 살펴보겠습니다.

- 노드(node) - 트리 안에 들어있는 각 항목을 말합니다.
- 자식 노드(child node) - 노드는 여러 자식 노드를 가질 수 있습니다.
- 부모 노드(parent node) - 노드 A가 노드 B를 자식으로 갖고 있다면, 노드 A를 노드 B의 '부모 노드'라고 부릅니다.
- 뿌리 노드(root node) - 트리의 가장 상층부에 있는 노드를 말합니다.
- 잎 노드(leaf node) - 자식 노드가 없는 노드를 말합니다.
- 조상 노드(ancestor node) - 노드 A의 자식을 따라 내려갔을 때 노드 B에 도달할 수 있다면, 노드 A를 노드 B의 조상 노드라고 부릅니다.
- 자손 노드(descendant node) - 노드 A가 노드 B의 조상 노드일 때, 노드 B를 노드 A의 자손 노드라고 부릅니다.
- 형제 노드(sibling node) - 같은 부모 노드를 갖는 다른 노드를 보고 형제 노드라고 부릅니다.



## DOM API

-Document Object Model, 문서 객체 모델

-HTML,XML문서를 프로그래밍하는 인터페이스

-JavaScript에만 있는 것이 아님



```javascript
//문서 전체에서 선택할 수 있는 다양한 메소드
document.queryselector
document.queryselectorAll
document.getElementById/ClassName/Name/TagName/NagNameNS

//요소 기준으로 선택하거나 찾는 메소드들
element.matches('#hplogo')
element.closest('div')//본인 포함해서 가장 가까운 것 찾기.queryselector랑 반대로 찾기

//queryselector 메소드를 활용한 결과는 NodeList
Array.isArray(document.querySelectorAll(element));
//false
document.querySelectorAll(element) instanceof NodeList
//true
```





```javascript

//element의 textcontent 삽입 가능
element.textContent='hello'


//항상 textContent를 쓰는게 좋고 innerHTML은 위험..
//Cross-Site Script 즉 해킹에 대한 위험이 있습니다.

// set/get/has/remove 등을 통해 Attribute의 value값을 변경,확인,삭제 등을 할 수 있습니다.
el.setAttribute('element','value');
console.log(el.getAttribute('element'))
console.log(el.hasAttribute('element'))
el.removeAttribute('element');

```



## 문제

1) 아래의 코드 입력 후 변수 foo를 console.log(foo)로 호출하면 나오는 결과를 고르시오. A:2

```javascript
function func() {
  var foo = 1;
}
func();
```

(1) 1	 (2) ReferenceError: foo is not defined 	(3) undefined 	(4) false



2)  변수명이 'a'이고 값이 '2'인 변수를 선언하고 싶다.  '스코프는 블록 스코프이며 '/'재대입이 가능하고'/'재선언이 불가하고 호이스팅이 작동하지 않는 ' 변수 설정 방법을 활용한 코드를 고르시오. A:3

(1) var a='2';	 (2) const a='2';	 (3) let a='2';	 (4) a='2';



3) 'this 바꿔치기' 에 관한 내용 중 **옳은 것**을 고르시오. A:2

(1) 함수 객체에 'bind' 메소드를 호출하면, 기존의 함수에서 메소드의 인자로 넘겨준 값이 this가 되는  함수로 변경된다. 

-새로운 함수가 반환됨. 변경 X

(2)  'apply' 메소드와 'call' 메소드의 기능은 동일하다.

(3) 'apply' 메소드와 'call' 메소드의 인자를 넘겨주는 형식은 같다.

-형식 다름(두번째 인자)

(4)  'this'를 우리가 원하는 값을 가리키게 만드는 메소드에는 'bind','call','apply','revise'가 있다.

-'revise'는 아님.



4)  아래의 코드를 실행했을때 출력되는 값을 고르시오. A:1

```javascript
function sum(...ns){
 return ns;
}

sum(1,2,3,4);
```

(1) [1,2,3,4]  	(2) {0:1, 1:2, 2:3, 3:4} 	(3) 1234 	(4) '1234'



5) 화살표 함수에 대한 설명 중 **옳지 않은** 것을 **모두** 고르시오. A: 1,2

 (1) 화살표 함수는 생성자로 사용될 수 있다.

-사용될 수 없다.

(2) 화살표 함수는 스스로의 this를 가질 수 있다.

-없다.

(3) 화살표 함수는 오직 **함수 혹은 메소드**로 사용되도록 만들어졌다.

(4) `function` 구문으로 생성되는 함수는 단순한 함수 이외에 생성자나 제너레이터 등의 여러 기능까지 떠맡고 있다.



