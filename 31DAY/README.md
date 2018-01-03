## 2018. 1. 2 수업내용

### Iterable

```js
// 분해대입
const [c1, c2] = 'hello'; // c1 = 'h' c2 = 'e'
```

### iterable 객체를 만들어내는 생성자들:

* String
* Array
* TypedArray
* Map
* Set

### Generator 함수

* `function*`

* iterable 을 편하게 만들어 낼 수 있다.

* 복잡해 보이지만 써보면 쉽다(고 하심)

* ```js
  const obj = {
    * gen() {
      // ...
    }
  }
  ```

* ```js
  function* numberGen() {
    yield 1;
    yield 2;
    yield 3;
  }

  // 1, 2, 3이 순서대로 출력
  for (let n of numberGen()) {
    console.log(n);
  }
  ```

* ```js
  function* numberGen() {
    yield 1;
    yield 2;
    yield 3;
  }

  function* numberGen2() {
    yield* numberGen();
    yield* numberGen();
  }

  // 1, 2, 3, 1, 2, 3이 순서대로 출력됩니다.
  for (let n of numberGen2()) {
    console.log(n);
  }
  ```

* array랑 비슷하지 않나? 왜 쓰는가?

* ```js
  // 이를테면 이런 게 가능
  function* range(start = 0, end = Infinity, step = 1) {
    for (let i = start; i < end; i += step) {
      yield i;
    }
  }

  for (let item of range(0,10)) {
  console.log(item);
  } // 0 1 2 ... 9

  for (let item of range(0,10,3)) {
  console.log(item);
  } // 0 3 6 9
  ```

* 배열로 만들기 까다로운 것들을 '계산' 해낼 수 있다.

* 주의점

  * Generator 함수로부터 생성된 iterable은 한 번만 사용될 수 있음.
    ```js
    function* gen() {
      yield 1;
      yield 2;
      yield 3;
    }

    const iter = gen();

    for (let n of iter) {
      // 잘 출력됨.
      console.log(n);
    }
    for (let n of iter) {
      // 실행되지 않음.
      console.log(n);
    }
    ```

  * Generator 함수 내부에서 정의된 일반 함수에서는 `yield`키워드를 사용할 수 없음.

    ```js
    // Generator 함수 내부에서 정의된 일반 함수에서는 `yield` 키워드를 사용할 수 없습니다.
    function* gen2() {
      // Unexpected token
      function* fakeGen() {
        yield 1;
        yield 2;
        yield 3;
      }
      fakeGen();
    }
    ```


### Iterator 프로토콜

* Iterable protocol을 만족하려면, `Symbol.iterator` 속성에 저장되어 있는 함수는 **iterator** 객체를 반환해야 함.

* Iterator 객체의 조건:

  * Iterator는 `next`라는 메소드를 갖는다.

  * `next` 메소드는 다음 두 속성을 갖는 객체를 반환해야 함.

    - `done` - 반복이 모두 끝났는지를 나타냅니다.
    - `value` - 현재 순서의 값을 나타냅니다.

* ```js
  const strIterator = 'go'[Symbol.iterator]();
  strIterator.next(); // { value: 'g', done: false }
  strIterator.next(); // { value: 'o', done: false }
  strIterator.next(); // { value: undefined, done: true }
  strIterator.next(); // { value: undefined, done: true }
  ```

* ```js
  function* gen() {
    yield 1;
    yield 2;
  }
  const genIterator = gen()[Symbol.iterator]();
  genIterator.next(); // { value: 1, done: false }
  genIterator.next(); // { value: 2, done: false }
  genIterator.next(); // { value: undefined, done: true }
  genIterator.next(); // { value: undefined, done: true }
  ```

### Generator 와 Iterator

1. generator 함수로부터 만들어진 객체는 **iterable protocol과 iterator protocol을 동시에 만족**
   * 'generator 객체에는 Symbol.iterator와 next 메소드가 다 있다' 고 기억해두자.

   ```js
   function* gen() {
     // ...
   }

   const genObj = gen();
   genObj[Symbol.iterator]().next === genObj.next; 	// true
   ```

2. 함수 실행을 중간에 멈추는 것이 가능

   ```js
   function* gen() {
     console.log('hello');
     yield 1;
     console.log('world');
     yield 2;
   }

   genObj = gen();
   genObj.next(); // hello
   genObj.next(); // world
   ```

3. generator 함수로부터 생성된 객체의 `next` 메소드에 인자를 주어서 호출하면, generator 함수가 멈췄던 부분의 `yield` 표현식의 결과값은 앞에서 받은 인자가 됨.

   ```js
   function* gen() {
     const received = yield 1;
     console.log(received);
   }

   const iter = gen();
   iter.next(); // { value: 1, done: false }

   // 'hello'가 출력됨.
   iter.next('hello'); // { value: undefined, done: true }
   ```

   * 인자를 이용해서 함수 바깥이랑 '통신'이 가능!

## Class

생성자의 기능을 대체하는 ES2015 신기능

```js
// 생성자
function Person({name, age}) {
  this.name = name;
  this.age = age;
}
Person.prototype.introduce = function() {
  return `안녕하세요, 제 이름은 ${this.name}입니다.`;
};
```

```js
// 클래스
class Person {
  // 이전에서 사용하던 생성자 함수는 클래스 안에 `constructor`라는 이름으로 정의합니다.
  constructor({name, age}) {
    this.name = name;
    this.age = age;
  }

  // 객체에서 메소드를 정의할 때 사용하던 문법을 그대로 사용하면, 메소드가 자동으로 `Person.prototype`에 저장됩니다.
  introduce() {
    return `안녕하세요, 제 이름은 ${this.name}입니다.`;
  }
}
```

* class는 함수가 아님.
* class는 객체도 아님.
* JS의 다른 곳에서는 사용되지 않는 별도의 문법을 사용함.
* 생성자 사용시 일어날 수 있는 전역 객체 오염이 문법적으로 방지됨.

### 인스턴스 메소드

클래스로 생성된 객체에 사용되는 메소드를 인스턴스 메소드로 부르기로 하자.

* ```js
  class Calculator {
    add(x, y) {
      return x + y;
    }
    subtract(x, y) {
      return x - y;
    }
  }
  ```

* 임의의 표현식을 **대괄호**로 둘러싸서 메소드의 이름으로 사용할 수도 있다.

* **Getter 혹은 setter**를 정의하고 싶을 때는 메소드 이름 앞에 `get` 또는 `set`을 붙여주면 된다.

* `static`키워드를 사용하여 정적 메소드를 만들 수도 있다.

* 메소드 이름 앞에 `*`를 붙여주면 generator 메소드를 정의 할 수 있다.

  ```js
  class Gen {
    constructor() {
      this.count = 0;
    }
    *[Symbol.iterator]() {
      while (true) {
      yield this.count++;
      }
    }
  }

  const genObj = new Gen();

  for (let n of genObj) {
    console.log(n);
    if (n > 10) break;
  }
  ```

**추천도서: 객체지향의 사실과 오해**

### 클래스필드

클래스 블록 안에서 할당 연산자(`=`)를 이용해 인스턴스 속성을 지정할 수 있는 문법.

(아마도) 다음 es 에서 공식 채택 될 것

```js
class MyClass {
  count = 0; // 클래스필드
  constructor(prop) {
  this.prop = prop;
  }
  inc() {
    this.count++; // .inc() count가 1씩 증가
  }
  desc = () => { // 객체가 만들어질 때 마다 새로 만들어짐
    this.count++; 
  }
}

MyClass.prototype.inc // [Function: inc]
MyClass.prototype.constructor // [Function: MyClass]
obj = new MyClass(); // MyClass { count: 0, prop: undefined}
Object.getPrototypeOf(obj); // MyClass {}
Object.getPrototypeOf(obj) === MyClass.prototype // true
obj.count // 0
Object.getPrototypeOf(obj).count // undefined

obj = new MyClass(1);
inc = obj.inc;
desc = obj.desc;
inc(); // this가 전역 객체를 가리킴
count // NaN
desc(); // this가 인스턴스를 가리킴
```

### 클래스 상속

한 클래스의 기능을 다른 클래스에서 **재사용**할 수 있다.

```js
class Parent {
  // ...
}

class Child extends Parent {
  // ...
}
```

- 자식 클래스 A를 통해 부모 클래스 B의 **정적 메소드와 정적 속성**을 사용할 수 있음.

- 부모 클래스 B의 **인스턴스 메소드와 인스턴스 속성**을 자식 클래스 A의 인스턴스에서 사용할 수 있음.

  ```js
  class Parent {
    static staticProp = 'staticProp';
    static staticMethod() {
      return 'I\'m a static method.';
    }
    instanceProp = 'instanceProp';
    instanceMethod() {
      return 'I\'m a instance method.';
    }
  }

  class Child extends Parent {}

  console.log(Child.staticProp); // staticProp
  console.log(Child.staticMethod()); // I'm a static method.

  const c = new Child();
  console.log(c.instanceProp); // instanceProp
  console.log(c.instanceMethod()); // I'm a instance method.
  ```

  ### super

  자식 클래스에서 같은 이름의 속성을 정의하면 부모 클래스의 속성이 가려짐

  ```js
  class Melon {
    getColor() {
      return '제 색깔은 초록색입니다.';
    }
  }

  class WaterMelon extends Melon {
    getColor() {
      return '속은 빨강색입니다.';
    }
  }

  const waterMelon = new WaterMelon();
  waterMelon.getColor(); // 속은 빨강색입니다.
  ```

  이런 경우, `super` 키워드를 통해 부모 클래스의 속성에 직접 접근 가능.

  ```js
  class Melon {
    getColor() {
      return '제 색깔은 초록색입니다.';
    }
  }

  class WaterMelon extends Melon {
    getColor() {
      return super.getColor() + ' 하지만 속은 빨강색입니다.';
    }
  }

  const waterMelon = new WaterMelon();
  waterMelon.getColor(); // 제 색깔은 초록색입니다. 하지만 속은 빨강색입니다.
  ```

  `super`

  - 생성자 내부에서 `super`를 함수처럼 호출 -> 부모 클래스의 생성자가 호출됨.
  - 정적 메소드 내부에서는 `super.prop`과 같이 써서 부모 클래스의 `prop` 정적 속성에 접근 가능함.
  - 인스턴스 메소드 내부에서는 `super.prop`과 같이 써서 부모 클래스의 `prop` 인스턴스 속성에 접근 가능함.

```js
class Person {
  constructor({name, age}) {
    this.name = name;
    this.age = age;
  }
  introduce() {
    return `제 이름은 ${this.name}입니다.`
  }
}

class Student extends Person {
  constructor({grade, ...rest}) {
    // 부모 클래스의 생성자를 호출할 수 있습니다.
    super(rest);
    this.grade = grade;
  }
  introduce() {
    // 부모 클래스의 `introduce` 메소드를 호출할 수 있습니다.
    return super.introduce() + ` 저는 ${this.grade}학년입니다.`;
  }
}

const s = new Student({grade: 3, name: '윤아준', age: 19});
s.introduce(); // 제 이름은 윤아준입니다. 저는 3학년입니다.
```

### 클래스 상속과 프로토타입 상속

```js
class Person {}
class Student extends {}
const student = new Student();
```

![class-inheritance-prototype-chain](/Users/suunohm/Downloads/class-inheritance-prototype-chain.svg)

## DOM 다시

html 요소에 정보를 저장하는 것이 가능하다.

data-index

data-count

data-key

```html
<div data-index="1" data-count="2" data-key="3"></div>
```
JS로 조작하는 것도 당연히 가능.
```js
const el = document.querySelector('div');
console.log(el.dataset.count);

el.dataset.key = '4';
el.dataset.password = 'asdf';
```

```html
<div data-msg="hello"></div>
```

```css
div::after {
  
}
```

### 노드 간 관계

- `el.childNodes`
- `el.firstChild`
- `el.lastChild`
- `el.previousSibling`
- `el.nextSibling`
- `el.parentNode`
- `el.offsetParent`

HTMLElement.offsetParent

pos: absolute인 자식의 pos: relative 인 부모를 선택하게 됨

### 엘리먼트 크기 및 위치

- `el.getBoundingClientRect()`
- `el.offsetHeight` / `el.offsetWidth`
- `el.clientHeight` / `el.clientWidth`
- `el.scrollHeight` / `el.scrollWidth`
- `el.offsetTop` / `el.offsetLeft`
- `el.scrollTop` / `el.scrollLeft`
- `el.clientTop` / `el.clientLeft`

집에 가서 한번씩 써보자!

## Event

### Capturing & Bubbling

![eventphases](/Users/suunohm/Downloads/eventphases.png)

capturing: DOM tree를 타고 내려옴

bubbling: DOM tree를 타고 올라감



그리하여:

```html
<div class="outer">
  <div class="inner">
    <button>버튼</button>
  </div>
</div>
```

```js
const outer = document.querySelector('.outer');
const inner = document.querySelector('.inner');
const button = document.querySelector('button');

outer.addEventListener('click', e => {
  alert('outer');
})
inner.addEventListener('click', e => {
  alert('inner');
})
button.addEventListener('click', e => {
  alert('button!');
})

// button -> inner -> outer 순서대로 반응
```

(addEventListener에 아무 옵션을 추가하지 않으면 bubbling 단계에서 반응함)

```js
const outer = document.querySelector('.outer');
const inner = document.querySelector('.inner');
const button = document.querySelector('button');

outer.addEventListener('click', e => {
  alert('outer');
}, true)
inner.addEventListener('click', e => {
  alert('inner');
}, true)
button.addEventListener('click', e => {
  alert('button!');
}, true)

// outer->inner->button 순서대로 반응
```

* 버블링이 일어나지 않는 이벤트도 있다 (blur, change, focus, submit 등등)

### 이벤트 객체

addEventListener에 console.log(e) 해보면 다양한 정보를 얻을 수 있음.

```js
document.querySelector('.outer').addEventListener('click', e => {
      console.log(e);
    })
```
* `e.target` `e.currentTarget`
  ```js
  document.querySelector('.outer').addEventListener('click', e => {
      console.log(e.target); // 실제로 클릭(이벤트가 일어난) 요소
      console.log(e.currentTarget); // 내가 eventListener를 등록한 요소
    })
  ```

* `e.stopPropagation()`

  ```js
  document.querySelector('.outer').addEventListener('click', e => {
        // console.log(e.target);
        // console.log(e.currentTarget);
        alert('outer clicked!');
      })
      document.querySelector('button').addEventListener('click', e => {
        alert('button clicked!');
        e.stopPropagation(); // 버블링 상관 없이 멈춤
      })
  ```

* `e.preventDefault()`

  ```js
  document.querySelector('a').addEventListener('click', e => {
        alert('a tag clicked!');
        e.preventDefault(); // href 링크로 넘어가지 않음
      })
  ```

### 마우스 이벤트

* mousedown <- 클릭 버튼이 눌렸을 때
* mouseup <- 눌렸다 떼어질 때
* mousemove <- 마우스 움직임

```js
const mouse = document.querySelector('.mouse');
mouse.addEventListener('mousedown', e => {
  console.log('mousedown');
})
mouse.addEventListener('mouseup', e => {
  console.log('mouseup');
})
mouse.addEventListener('mousemove', e => {
  console.log(e.clientX, e.clientY); // 마우스 포인터 좌표가 로깅 됨
})
```

박스 드래그 구현 해보자!