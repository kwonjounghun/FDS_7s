# 2017년 12월 8일 강의내용 정리

## Session

### 1. 자료구조

1. 데이터를 어떻게 체계적으로 저장할 지에 관한 것이다.
2. 배열, Stack, Tree 등이 있다.
3. 자료구조와 알고리즘을 알고 있으면 사용할 라이브러리에 대해서 제대로 알고 사용할 수 있다.

<br />

### 2. Array.prototype.includes()

1. String 래퍼 객체와 마찬가지로 `includes()` 메소드를 사용할 수 있다.

   ```javascript
   const arr = [1, 2, 3, 4, 5]
   arr.includes(1) // true
   ```

<br />

### 3. 자바스크립트에서 정수 나눗셈을 다루는 방법

1. `Math.floor(a / b)`를 이용하여 정수 나눗셈을 처리할 수 있다.

<br />

### 4. 버블 정렬 알고리즘

1. 배열의 각 요소를 순차적으로 두 개씩 비교해보면서 큰 값을 뒤로 보내는 방법이다.

<br />

### 5. String.prototype.toUpperCase, String.prototype.toLowerCase

1. `String.prototype.toUpperCase`는 문자열을 모두 소문자로 변환한 새로운 문자열을 반환한다. 이때 원본 문자열은 바뀌지 않는다.
2. `String.prototype.toLowerCase`는 문자열을 모두 소문자로 변환한 새로운 문자열을 반환한다. 이때 원본 문자열은 바뀌지 않는다.

<br />

### 6. String.prototype.repeat()

1. 파라미터로 전달된 문자열을 반복할 수 있다.

   ```javascript
   ' '.repeat(3) + 'hello' // '   hello'
   ```

<br />

### 7. 문자열과 배열

1. 문자열을 배열처럼 다룰 수 있다.

   ```javascript
   const str = 'string'

   for (const char of str) {
     console.log(char);
   }
   ```

<br />

### 8. key in Object

1. key in Object 형식으로 속성의 존재 여부를 확인할 수 있다.

   ```javascript
   const obj = { name: 'Lee' }
   name in obj // true
   ```

<br />

<br />

## Algorithm 문제 풀이

### Array

#### 문제 4

배열을 입력받아, 중복된 요소가 제거된 새 배열을 반환하는 함수를 작성하세요.

```javascript
// My Code
const set = arr => {
  arr.forEach((item, index) => {
    for (let i = arr.length - 1; i > index; i--) {
      if (item == arr[i]) {
        arr.splice(i, 1);
      }
    };
  })
   return arr;
}

// Solution
function removeDuplicates(arr) {
  const newArr = [];
  for (let item of arr) {
    if (!newArr.includes(item)) {
      newArr.push(item);
    }
  }
  return newArr;
}
```

<br />

#### 문제 5

수 타입의 값으로만 이루어진 두 배열을 입력받아, 다음과 같이 동작하는 함수를 작성하세요.

- 두 배열의 같은 자리에 있는 요소를 더한 결과가 새 배열의 요소가 됩니다.
- 만약 입력받은 두 배열의 길이가 갖지 않다면, 긴 배열에 있는 요소를 새 배열의 같은 위치에 포함시키세요.

예:

```
addArray([1, 2, 3], [4, 5, 6, 7]) -> [5, 7, 9, 7]
```

```javascript
// My Code
const addArray = (a, b) => {
  const newArray = [];
  const newLength = a.length < b.length ? a.length : b.length;

  for (let i = 0; i < newLength; i++) {
    newArray[i] = a[i] + b[i];
  }

  if (a.length > b.length) {
    for (let i = newLength; i < a.length; i++) {
      newArray[i] = a[i];
    }
  } else if (a.length < b.length) {
    for (let i = newLength; i < b.length; i++) {
      newArray[i] = b[i];
    }
  }

  return newArray;
}

// Reverse
const reverse = arr => {
  const reversedArray = [];
  for (let i = arr.length - 1; i >= 0; i--) {
    reversedArray.push(arr[i]);
  };
  return reversedArray;
};

// Solution
function addArray(arr1, arr2) {
  const newArr = [];
  const longArr = arr1.length > arr2.length ? arr1 : arr2;
  const shortArr = arr1.length > arr2.length ? arr2 : arr1;
  
  for (let i = 0; i < longArr.length; i++) {
    newArr.push(longArr[i]);
    if (shortArr[i] !== undefined) {
      newArr[i] += shortArr[i]
    }
  }
  return newArr;
}

// Reverse Solution
function reverse(arr) {
  const newArr = [];
  
  for (let i = arr.length - 1; i >= 0; i++) {
    newArr.push(arr[i]);
  }
  return newArr;
}
```

<br />

#### 문제 6

배열을 입력받아, 배열의 요소 중 두 개를 선택하는 조합을 모두 포함하는 배열을 작성하세요.

예:

```
combination([1, 2, 3]); -> [[1, 2], [1, 3], [2, 3]]
```

```javascript
// My Code
const combination = arr => {
  const result = [];

  for (let i = 0; i < arr.length - 1; i++) {
    for (let j = i + 1; j < arr.length; j++) {
      const item = [];
      item.push(arr[i], arr[j]);
      result.push(item);
    }
  }
  return result;
}

// Solution

```

<br />

#### 문제 7

'금액'과 '동전의 종류가 들어있는 배열'를 입력받아, 최소한의 동전을 사용해서 금액을 맞출 수 있는 방법을 출력하는 함수를 작성하세요.

예:

```
coins(163, [100, 50, 10, 5, 1]);
// 출력
100
50
10
1
1
1
```

```javascript
// My Code
const coins = (money, coin) => {
  const sortedCoin = coin.sort((x, y) => y - x)
  let rest = money;
  let quotient = 0;

  for (let i = 0; i < sortedCoin.length; i++) {
    rest = i == 0 ? money : rest % sortedCoin[i - 1];
    quotient = Math.floor(rest / sortedCoin[i]);
    for (let j = 0; j < quotient; j++) {
      console.log(sortedCoin[i]);
    }
  }
}

// or
const coins2 = (money, coin) => {
  let rest = money;
  const sortedCoin = coin.sort((x, y) => y - x);

  for (const item of coin) {
    
    while (rest >= item) {
      rest -= item;
      console.log(item);
    }
  }
}

// Solution
function coins(amount, coinTypes) {
  let currentAmount = amount;
  for (let ct of coinTypes) {
    // 정수 나눗셈 방법
    const result = Math.floor(currentAmount / ct);
    
    // 코인타입을 result만큼 출력
    // ...
    for (let i = 0; i < result; i++) {
      console.log(ct)
    }
    // 빼기
    // ...
    currentAmount -= result * ct;
  }
}

// Solution 2
function coins2(amount, coinTypes) {
  let currentAmount = amount;
  for (let ct of coinTypes) {
    while (currentAmount - ct > 0) {
      console.log(ct);
      currentAmount -= ct;
    }
  }
}
```

<br />

#### 문제 8

수 타입의 값만 들어있는 배열을 입력받아, 해당 배열을 오름차순 정렬하는 함수를 작성하세요. (`Array.prototype.sort`를 사용하지 않고 작성해보세요. [선택 정렬](https://ko.wikipedia.org/wiki/%EC%84%A0%ED%83%9D_%EC%A0%95%EB%A0%AC)을 참고하세요.)

```javascript
// My Code
const sort = arr => {
  let temp;
  for (let i = 0; i < arr.length-1; i++) {
    for (let j = i + 1; j < arr.length; j++) {
      if (arr[i] > arr[j]) {
        temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
      }
    }
  }
  console.log('배열이 변경되었습니다.')
}

// Solution
function sort(arr) {
  for (let i = 0; i< arr.length; i++) {
    let min = arr[i];
    let minIndx = i;
    for (let j = i + 1; j < arr.length; j++) {
      // 지금 탐색중인 값이 최소값인지 검사하기
      if (min > arr[j]) {
        // 최소값과 인덱스를 기억하기
        min = arr[j];
        minIndex = j;
      }
    }
    // 자리 바꾸기
    // const temp = arr[minIndex];
    // arr[minIndex] = arr[i];
    // arr[i] = temp;
    
    [arr[i], arr[minIndex]] = [arr[miinIndex], arr[i]];
  }
}
```

<br />

### String

#### 문제 1

두 문자열을 입력받아, 대소문자를 구분하지 않고(case insensitive) 두 문자열이 동일한지를 반환하는 함수를 작성하세요.

예:

```
insensitiveEqual('hello', 'hello'); -> true
insensitiveEqual('hello', 'Hello'); -> true
insensitiveEqual('hello', 'world'); -> false
```

```javascript
// My Code
const insensitiveEqual = (a, b) => {
  return a.toLowerCase() === b.toLowerCase() ? true : false
}

// Solution
function insensitiveCompare(str1, str2) {
  return str1.toLowerCase() === str2.toLowerCase();
}
```

<br />

#### 문제 2

문자열 `s`와 자연수 `n`을 입력받아, 만약 `s`의 길이가 `n`보다 작으면 `s`의 왼쪽에 공백으로 추가해서 길이가 `n`이 되게 만든 후 반환하고, 아니면 `s`를 그대로 반환하는 함수를 작성해보세요.

예:

```
leftPad('hello', 8); -> '   hello'
leftPad('hello', 3); -> 'hello'
```

```javascript
// My Code
const leftPad = (str, num) => {
  if (str.length < num) {
    let space = '';
    while (true) {
      space += ' ';

      if (space.length == num - str.length) {
        break;
      }
    }
    str = space + str;
  }
  return str;
}

// Solution
function leftPad(s, n) {
  if (s.length > n) {
    return s;
  } else {
    return ' '.repeat(n - s.length) + s;
  }
}
```

<br />

#### 문제 3

문자열을 입력받아, 문자열 안에 들어있는 모든 모음(a, e, i, o, u)의 갯수를 반환하는 함수를 작성하세요.

```javascript
// My Code
const vowel = str => {
  let count = 0;
  for (const char of str) {
    switch (char) {
      case 'a':
      case 'e':
      case 'i':
      case 'o':
      case 'u':
        count++;
      default:
    }
  }
  return count;
}

// Solution
```

<br />

#### 문제 4

문자열을 입력받아, 해당 문자열에 포함된 문자의 종류와 갯수를 나타내는 객체를 반환하는 함수를 작성하세요.

예:

```
countChar('tomato'); -> {t: 2, o: 2, m: 1, a: 1}
```

```javascript
// My Code
const countChar = str => {
  const obj = {};
  const split = str.split('');
  split.forEach((item, index) => {
    if (!obj.hasOwnProperty(item)) {
      obj[item] = 1;
    } else {
      obj[item]++
    }
  })

  return obj;
}

// Solution
function countChar(str) {
  const obj = {};
  for (let c of str) {
    if (c in obj) {
      obj[c]++;
    } else {
      obj[c] = 1;
    }
  }
  return obj;
}
```

<br />

<br />

## Quiz

1. 다음 코드를 확인한 후 **옳은 설명**을 모두 고르세요.

   ```javascript
   const style = {
     'margin': '30px',
     'padding-left': '10px',
     color: 'blue'
   }

   const display = 'grid';
   ```

   1. `style.margin`을 실행하면 style 객체의 margin 값인 '30px'을 얻을 수 있다.
   2. `style.padding-left`을 실행하면 style 객체의 padding-left 값인 '10px'을 얻을 수 있다.
   3. `style[color]`을 실행하면 style 객체의 color 값인 'blue'를 얻을 수 있다.
   4. `style[display] = 'flex'`을 실행하면 style 객체에 `{ display: 'flex' }`와 같이 display라는 프로퍼티명으로  'flex'라는 값이 추가된다.

   <br />

   정답: ①

   해설

   ② - 자바스크립트에서 유효한 의미를 갖는 프로퍼티에 접근할 때에는 대괄효 표기법으로 호출해야 한다. **자바스크립트는 `-`를 style.padding과 padding을 빼는 연산자로 인식**한다. 따라서 padding-left 프로퍼티에 접근하기 위해서는 `style['padding-left']`로 접근하여야 한다.

   ③ - 대괄호 표기법으로 프로퍼티를 호출할 때, 읽어들일 값을 ''(따옴표)로 감싸지 않으면 해당 값을 변수명으로 인식한다. 따라서 `style[color]`로 호출할 때 자바스크립트는 `color`를 변수명으로 인식하지만 `color` 변수를 정의한 적이 없기 때문에 Refference Error를 발생시킨다.  

   ④ - `style[display] = 'flex'`에서 대괄호 안의 `display`를 따옴표로 감싸지 않았으므로 자바스크립트는 `display`를 변수명으로 인식한다. 이때 `display` 변수에 할당된 값은 문자열이고, `style` 객체에 `{ grid: 'flex' }`가 추가된다.

   <br />

2. `obj` 객체에 `name` 프로퍼티가 존재하는지 확인하기 위한 방법은?

   1. `obj in name`
   2. `const obj in name`
   3. `name in obj`
   4. `const name in obj`

   <br />

   정답: ③

   해설: `프로퍼티명 in 객체명` 형식으로 객체 내의 프로퍼티 존재 여부를 확인할 수 있다.

   <br />

3. 다음 보기 중 Number 타입의 두 변수 `a, b`에 대하여 `a` 를 `b`로 나눈 **몫**을 구하기 위한 코드로 올바른 것은?

   1. `a / b`
   2. `a % b`
   3. `Number.ceil(a / b)`
   4. `Number.floor(a / b)`
   5. `Number.floor(a % b)`

   <br />

   정답: ④

   해설:  `/`는 나눗셈 연산자, `%`는 나머지 연산자를 의미한다. 이때 자바스크리브는 정수를 나타내는 자료형이 따로 존재하지 않기 때문에, 몫을 구하기 위해서는 `/` 연산 실행 후 `Number.prototype.floor()`을 이용하여 소수점 이하 자리를 버려야 한다.

   <br />

4. Math 객체의 메소드로 옳은 것을 모두 고르시오.

   1. `max()`
   2. `sum()`
   3. `PI()`
   4. `random()`
   5. `floor()`

   <br />

   정답: ①, ③, ④, ⑤

   <br />

5. 문자열에 사용할 수 있는 메소드를 모두 고르시오.

   1. `includes()`
   2. `length()`
   3. `toUpperCase()`
   4. `repeat()`
   5. `filter()`

   <br />

   정답: ①, ③, ④, ⑤