# JAVASCRIPT 심화

## 함수형 프로그래밍 (Functional Programming)

***shared mutable state*** => 지양해야 하는 상태

### 고차 함수 (Higher-order Function)

함수를 인자(콜백_callback)로 받는 함수, 또는 함수를 반환하는 함수

ex) ```Array```의 많은 메소드들(`forEach`, `map`, `reduce`, `filter`, `sort`, `every`, `some`, `find` 등)

**클로저(Closure)**: 고차 함수에서 안쪽 스코프에서 **바깥 스코프에 있는 변수를 가져다 사용하는 함수와 변수가 저장되는 저장소**로 이러한 클로저의 특징을 활용하여 **데이터는 숨기고 정해진 방법을 통해서만 데이터에 접근할 수 있도록 하는 고차 함수를 작성**할 수 있습니다.

화살표 함수 문법을 이용하면 적은 양의 코드로 고차 함수를 만들 수 있습니다.

**재귀 함수 (Recursive Function)**: 함수 내부에서 **자기 자신을 호출하는 함수**

------

## 객체 더 알아보기

### 객체 자신의 속성 (Own Property)

상속받은 객체는 상속받은 속성(inherited property)과 자신의 속성(own property)을 반환할 수 있다.

```객체.속성명```, ```속성명 in 객체``` 로 속성에 접근하거나 판단한다면 **상속받은 속성과 자신의 속성을 구분할 수 없다.**

```객체.hasOwnProperty(속성명)```을 이용하여 객제 자신이 어떤 속성을 가지고 있는지 확인할 수 있다.



### 데이터 속성( Data Property)의 부수속성(Property Attribute)

객체의 속성마다 동작 방식이 다를 수 있는데 이 정보는 속성의 부수속성(property attribute)에 담겨 있다.

**속성 기술자(property descriptor)**: ```객체.getOwnPropertyDescriptor```라는 정적 메소드를 사용해 부수속성을 나타내는 객체

**데이터 속성(data property)에 대한 속성 기술자의 속성**

- value: 속성에 어떤 값이 저장되어 있는지
- writable: 변경할 수 있는 속성인지 (Boolean type)
- enumerable: 열거 가능한 속성인지 (Boolean type)
- configurable: 부수속성을 변경, 삭제할 수 있는지 (Boolean type)

```Object.getOwnPropertyDescriptor(객체)```: 객체 전체 속성에 대한 속성 기술자를 반환 

### 속성 기술자를 통해 객체의 속성 정의하기

- ```Object.create(생성할 객체의 프로토타입이어야 할 객체, 생성할 객체에 추가될 속성 설명자)```

  [ MDN Object.create ]: https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/create

- ```Object.defineProperty(속성을 정의 할 객체, 정의 하거나 수정할 속성명, 정의하거나 수정하려는 속성에 대한 속성 설명자)```

  [ MDN Object.defineProeprty ]: https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty

- ```Object.defineProperties(속성을 정의 할 객체, 추가할 속성들의을 객체타입으로 열거)```

  [MDN Object.defineProperties]: https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperties

### 접근자 속성(Accessor Property)과 그 부수속성

접근자 속성(Accessor property): getter와 setter가 정의된 속성

**접근자 속성(Accessor Proeprty)의 속성 기술자의 속성**

- ```get```: getter 함수. 속성을 읽어올 때 호출.
- ```set```: setter 함수. 속성을 변경할 때 호출.
- ```enumerable```: 열거 가능한 속성인지
- ```configurable```: 부수속성을 변경, 삭제할 수 있는지

getter, setter를 활용하면 속성처럼 사용할 수 있지만 다른 함수를 거치지 않고 데이터를 가공할 수 있다.

### 객체의 속성 열거하기

```enumerable```속성: 객체의 속성을 열거할 때 그 결과에 영향을 준다.

- ```Object.keys```: 객체 자신의 속석 중 열거 가능한 속성의 이름을 배열로 반환
- ```Object.values```: 객체 자신의 속성 중 열거 가능한 속성의 속성 값을 배열로 반환합니다.
- ```Object.entries```: 객체 자신의 속성 중 열거 가능한 속성의 속성 값을 배열로 반환합니다.
- ```Object.getOwnPropertyNames```: 객체 자신의 모든 속성의 이름을 배열로 반환합니다. **열거 불가능한 속성도 포함**
- ```for...in```구문: 객체 자신의 속성 및 상속받은 속성 중 열거 가능한 속성의 이름을 배열로 반환합니다.

### 얕은 복사(Shallow Copy) & 깊은 복사(Deep Copy)

```Object.assign```: 인자로 받은 객체들의 모든 열거 가능한 속성을 대상 객체에 복사합니다. 빈 객체를 대상으로 사용하면 객체를 복제할 수 있습니다.

**깊은 복사(deep copy)**: 객체에 대한 참조뿐만 아니라 중첩된 자료구조까지 모두 복사하는 것 

### 객체 속성 추가 제어하기 ```[[Extensible]]```

JS의 모든 객체에 숨겨진 속성인 ```[[Extensible]]```의 값에 따라 객체에 속성을 추가할 수 있게 하거나 속성 추가를 막을 수 있습니다.

- ```Object.preventExtensioins(객체)```: 객체의 ```[[Extensible]]```을 ```false```로 바꿔 객체에 속성을 추가할 수 없게 한다.
  - ```Object.isExtensible```: ```[[Extensible]]```의 속성 값을 반환
- ```Object.seal(객체)```: 객체의 ```[[Extensible]]``` 속성을 ```false```로 바꾸고, 객체 자신의 속성을 모두 ```configurable: false``` 상태로 바꾼다.
  - ```Object.isSealed```: 객체가 확장 불가능하고 객체 자신의 모든 속성에 대한 부수속성이 ```configurable: false```에 해당하면 ```true``` 아니면 ```false```를 반환한다.
- ```Object.freeze(객체)```: 객체의 ```[[Extensible]]``` 속성을 ```false```로 바꾸고, 객체 자신의 속성을 모두 ```configurable: false, writable: false ```상태로 바꾼다.
  - ```Object.isFrozen```: 객체가 확장 불가능하고 객체 자신의 모든 속성에 대한 부수속성이 ```configurable: false, writable: false```에 해당하면 ```true``` 아니면 ```false```를 반환한다.

------

## 연산자 더 알아보기

### 표현식(Expression)

코드 중에 값으로 변환될 수 있는 부분

- 리터럴
  - `1`
  - `null`
  - `'hello'`
  - `{prop: 1}`
  - `[1, 2, 3]`
  - `function(x, y) { return x + y }`
  - `(x, y) => x + y`
- 연산자
  - `1 + 2`
  - `true && false`
  - `'prop' in obj`
  - `delete obj.prop`
  - `typeof null`
  - `obj instanceof Object`
  - `new Object()`
  - (`variable` 변수가 선언되어 있다면) `variable = 1`
- 기타
  - `this`
  - `variable` (변수)
  - `obj.prop` (속성)
  - `func()` (함수 호출)

평가(evaluation): 표현식을 실행시키는 절차

### Short-circuit Evaluation

피연산자가 두 개인 연산 중에, 값을 결정하기 위해 양쪽 피연산자 모두가 필요하는 않은 경우에 하나의 피연산자만 평가하는 방식으로 코드 길이를 줄일 수 있는 이점이 있지만 의미와 논리가 부족해지는 부분이 생길 수 있습니다.

### 삼항 연산자(Ternary Operator)

```a ? b : c```와 같이 표현하는 표현식으로 ```a```가 truthy이면 ```b```가 falsy이면 ```c```가 반환됩니다. 삼항연산자로 간단한 ```if...else```구문을 대신할 수 있습니다.

### 증가/감소 연산자 (Increment/Decrement Operator)

```n++```, ```n--``` 표현식은 값을 증가, 감소시키기 전의 피연산자를 그대로 반환합니다.

```++n```, ```--n``` 표현식은 값을 증가 감소시킨 결과를 반환합니다.

### 할당 연산자 (Assignment Operator)

```=```, ```+=```, ```-=```의 연산자에 대한 표션식의 결과값은 왼쪽 피연산자에 실제로 할당된 값이 됩니다.

### 연산자 우선 순위 (Operator Precedence)

다수의 연산자가 있을 경우 연산자 우선 순위에 따라 계산됩니다.

코드 가독성과 우선 순위의 가독성을 높이기 위해 괄호로 둘러 싸주는 것이 좋습니다.

[ MDN 연산자 우선순위 ]: https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/%EC%97%B0%EC%82%B0%EC%9E%90_%EC%9A%B0%EC%84%A0%EC%88%9C%EC%9C%84

### 연산자 결합 순서 (Operator Associativity)

대부분의 연산의 경우 결합 순서가 명시적이지만 **거듭제곱, 할당, 삼항 연산자는 우결합성을 가진다.**

### 값을 비교하는 여러가지 방법

- ```==```, ```!=```
- ```===```, ```!==```
- ```Object.is```

#### 추상적 동일성 (Abstract Equality)

```==``` 연산자는 두 피연산자의 타입이 다를 때는 타입을 변환한 후 비교합니다. null check에 유용하게 사용되지만 그 외의 경우에는 타입을 변환하는 과정에서 의도치 않은 동작을 하지 않도록 유의하여 사용해야 합니다.

```==```연산자는 ```null```과 ```undefined```를 동일하지만 다른 어떤 값과도 동일하지 않은 것으로 취급합니다.

#### 엄격한 동일성 (Strict Equality)

```===```, ```!==``` 연산자는 두 피연산자의 타입이 다른 경우 무조건 ```false```를 반환합니다.

**Number 타입 비교 시의 예외**

- ```NaN === NaN; //false```
- ```0 === -0; //true```

#### Object.is

두 인자가 정말로 같은 값인지 검사하는 메소드로 예외를 제외하고는 ```===```연산자와 같은 역할을 합니다.

**Object.is 타입 비교 시의 예외**

- ```Object.is(NaN, NaN); //true```
- ```Object.is(0,-0); //false```

------

#  QUIZ

Q1. obj객체 자신의 속성으로 'ownProp'이 있는지 확인할 수 있는 방법으로 옳은 것은?

1. **obj.hasOwnProperty('ownProp');**
2. ('ownProp' in obj)
3. (obj.ownProp === ownProp)
4. (obj.ownProp === 'ownProp' in obj)

Q2. 다음의 코드를 실행 후, 보기의 실행문의 결과로 반환되는 배열의 길이가 다른 하나를 고르세요.

```javascript
const obj = Object.create(Object.prototype, {
  prop1: {
    value: 1,
    writable: false,
    enumerable: true,
    configurable: false
  },
  prop2: {
    value: 2
  }
});

const obj2 = Object.create(obj, {
  prop3: {
    value: 3,
    writable: true,
    enumerable: true
  },
  prop4: {
    value: 3,
    writable: true
  }
});
```

1. Object.keys(obj2).length;
2. Object.values(obj2).length;
3. Object.entries(obj2).length;
4. **Object.getOwnProeprtyNames(obj2).length;**

Q3. 다음의 코드를 실행 후, 보기의 실행문을 실행한 결과가 다른 하나를 고르세요.

```javascript
const obj = {
  innerObj: {
    a: 'apple',
    b: 'bear'
  }
};

const obj2 = Object.assign({}, obj);
obj.innerObj.a = 'airplane';
```

1. console.log(obj.innerObj === obj2.innerObj)
2. **console.log(obj2.innerObj.a === 'apple')**
3. console.log(obj !== obj2)
4. console.log(obj.innerObj.a === 'airplane')

Q4. 객체를 다음과 같이 freeze 시켰을 때, 보기의 실행문의 결과가 다른 하나를 고르세요.

```javascript
const obj = {};
Object.freeze(obj);
```

1. console.log(Object.isFrozen(obj));
2. console.log(Object.isSealed(obj));
3. **console.log(Object.isExtensible(obj));**
4. console.log(!Object.isExtensible(obj));


Q5. 결과 값이 true인 표현식을 모두 고르세요.

NaN === NaN	**Object.is(NaN, NaN)**		**0===-0**		Object.is(0,-0)	null===undefined	typeof 'abcd' === 'ab' + 'cd'	**(0)?false:true**