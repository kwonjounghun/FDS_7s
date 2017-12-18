## 수업 내용

* 문자열을 배열로 바꾸기

  ```javascript
  [...'hello'];
  Array.from('hello');
  'hello'.split('');
  // 결과는 모두 ['h', 'e', 'l', 'l', 'o'] 로 출력됩니다

  'hello'[0];
  //위처럼 String을 배열처럼 접근 할 수 있습니다. 결과값은 'h'
  ```

* String 특정문자열이 포함됐는지 확인하는 method

  ```javascript
  'hello javascript'.includes('hello'); // true
  'hello javascript'.startsWith('he'); // true
  'hello javascript'.endsWith('ript'); // true
  'hello javascript'.search('java'); // 6
  ```

* slice와 splice 차이

  * slice : index의 값 사이에서 추출한다고 이해 

  ```
  str.slice(beginIndex[, endIndex])
  ```


  ```js
  const str = 'bingomani'
  str.slice(2,3) // 2번째 index인 'i'에서 시작해서 3번째 index인 'n'사이 끝내서 그 값을 추출한다.
  //결과값은 n

  ```

  * splice : start의 index값을 잘라낸다고 이해

  ```javascript
  array.splice(start, deleteCount)
  ```

  ```javascript
  const str = 'bingomania'
  str.splice(2,3) // 2번째 index인 'i'에서 시작해서, 3개를 잘라낸다.
  //결과값은 bimania

  ```

* const: const는 const에 지정된 값이 바뀌는 것을 막아주는 것이 아니라 '재대입'을 되지 않게 하는 것. 

  ```js
  const arr = [1, 2, 3, 4, 5];
  arr.splice(1, 3); // [2, 3, 4]
  console.log(arr); // [ 1, 5]
  ```

------

## Basic 문제

### 문제 1

두 수를 입력받아 큰 수를 반환하는 함수를 작성하세요.

```javascript
function getBigger(n1, n2) {
  //n1이 n2 이상일 경우 n1을 반환하고 n1이 n2보다 작을 때 n2를 반환한다.
	return (n1 >= n2)?n1:n2;
}
```



### 문제 2

세 수를 입력받아 그 곱이 양수이면 `true`, 0 혹은 음수이면 `false`, 둘 다 아니면 에러를 발생시키는 함수를 작성하세요.

```javascript
function getPositive(n1, n2, n3) {
	//입력받은 값의 곱을 val 상수에 대입
  	const val = n1*n2*n3;
	if(val > 0){//val이 양수이면 true를 반환
		return true;
	}else if(val <= 0){//val이 0또는 음수이면 false를 반환
		return false;
	}else {//유효하지 않은 값이 들어왔을 경우(NaN) 에러 발생
		throw new Error("Error!");
	}
}
```



### 문제 3

세 수 `min`, `max`, `input`을 입력받아, 다음과 같이 동작하는 함수를 작성하세요.

- `min`보다 `input`이 작으면, `min`을 반환합니다.
- `max`보다 `input`이 크면, `max`를 반환합니다.
- 아니면 `input`을 반환합니다.

예:

```
limit(3, 7, 5); -> 5
limit(3, 7, 11); -> 7
limit(3, 7, 0); -> 0
```

```javascript
function limit(min, max, input){
  if(input < min){//input 값이 min보다 작으면 min 반환
    return min;
  }else if(input > max){//input 값이 max보다 크면 max 반환
    return max;
  }else{//input이 min과 max의 사이 값이면 input 반환
    return input;
  }
}
```



### 문제 4

어떤 정수가 짝수인지 홀수인지 출력하는 함수를 작성하세요. 이를 이용해서, 1부터 20까지의 수가 각각 짝수인지 홀수인지 출력하는 프로그램을 작성하세요.

```javascript
//짝수, 홀수 판별 함수
function judgeNumber(n) {
  //(n%2 === 0) 짝수를 의미하므로 n을 2로 나눈 나머지가 0이면 Even, 0이 아닌 경우 Odd를 반환
	return (n%2 === 0)?"Even":"Odd";
}
```

```javascript
//1~n까지의 숫자의 짝수, 홀수를 판별하여 출력하는 함수
function judgeNumbers(n) {
	for(let i = 1; i <= n; i++){
		console.log(`${i} is ${judgeNumber(i)}`);
	}
}
```



### 문제 5

100 이하의 자연수 중 3과 5의 공배수를 모두 출력하는 프로그램을 작성하세요.

```javascript
function cmMultiple() {
  //i를 1부터 100까지 1씩 증가시키며
	for(let i = 1; i <= 100; i++){
      //i를 3으로 나눈 나머지가 0이고 i를 5로 나눈 나머지가 0인 경우 그 값 i를 출력
		if(i%3 === 0 && i%5 === 0){
			console.log(i);
		}
	}
}
```



### 문제 6

자연수를 입력받아, 그 수의 모든 약수를 출력하는 함수를 작성하세요.

```javascript
function printFactors(n) {
  //i를 1부터 100까지 1씩 증가시키며
	for(let i = 1; i <= n; i++){
      //입력받은 n을 i로 나눈 나머지가 0이면(=약수이면) i를 출력 
		if(n%i === 0)
		{
			console.log(i);
		}
	}
}
```



### 문제 7

2 이상의 자연수를 입력받아, 그 수가 소수인지 아닌지를 판별하는 함수를 작성하세요.

```javascript
function isPrime(n) {
  //2부터 n-1까지 1씩 증가하며
  for(let i = 2; i <= n-1; i++){
    //입력받은 값 n을 i로 나눈 나머지가 0이 나올 경우 false를 반환 (1과 n 외의 약수가 있는 경우에는 소수가 될 수 없음)
    if(n%i === 0)
    {
      return false;
    }
  }
  //for문을 모두 반복 후에 반환된 값이 없다면 소수이므로 true값을 반환
  return true;
}
```



### 문제 8

1부터 100까지의 수를 차례대로 출력하되, 자릿수에 3, 6, 9중 하나라도 포함되어 있으면 '짝!'을 대신 출력하는 프로그램을 작성하세요.

```javascript
function playTSN() {
	let val = "";
  	let str = "";
	//1부터 100까지 1씩 증가하며 반복
  	for(let i = 0; i < 101; i++){
      //i를 문자열로 바꾼다
      str = i.toString();
      //숫자를 문자열로 바꾸고 해당 값에 3,6,9가 포함되어 있는지 확인하여 포함되어 있을 경우 "짝!"을 출력하고 없을 경우 숫자를 출력한다.
      //if(str.includes("3") || str.includes("6" || str.includes("9")))
		if(str.search(/[3,6,9]/) > -1){
			console.log("짝!");
		}else{
			console.log(i);
		}	
	}
}
```



### 문제 9

양의 정수를 입력받아, 다음과 같은 패턴의 출력을 하는 함수를 작성하세요.

1을 입력받은 경우:

```
*
```

3을 입력받은 경우:

```
*
* *
* * *
```

5를 입력받은 경우:

```
  0 1 2 3 4 
0 *
1 * *
2 * * *
3 * * * *
4 * * * * *
```

```javascript
/*
	피라미드 모양을 grid에 넣는 다고 생각하고
	i는 row, j는 column으로 이해하면 좋을 것 같습니다.
*/
function buildHalfPyramid(n) {
	let ret = "";
  	//i는 0부터 n보다 작을 때까지 1씩 증가하며 반복
	for(let i = 0; i < n; i++){
      //j는 0부터 i까지 1씩 증가하며 반복하며 "*"을 변수에 추가
		for(let j = 0; j <= i; j++){
			ret += "*";
		}
      //j만큼 반복 후 줄바꿈
		ret += "\n";	
	}
	return ret;
}
```



### 문제 10

양의 정수를 입력받아, 다음과 같은 패턴의 출력을 하는 함수를 작성하세요.

1를 입력받은 경우:

```
*
```

3를 입력받은 경우:

```
  *
 * *
* * *
 * *
  *
```

5를 입력받은 경우:

```
  12345
1     *
2    * *
3   * * *
4  * * * *
5 * * * * *
4  * * * *
3   * * *
2    * *
1     *
```

```javascript
function buildDiamond(n) {
	let ret = "```\n";
	let i, j, k;
	for(i = 0; i < n; i++){
		for(k = 0; k < n-i; k++){
			ret += " ";
		}
		for(j = 0; j < i; j++){
			ret += "* ";
		}
		ret += "\n";
	}
	for(i; i > 0; i--){
		for(k = 0; k < n-i; k++){
			ret += " ";
		}
		for(j = 0; j < i; j++){
			ret += "* ";
		}
		ret += "\n";
	}
	ret += "```";
	return ret;	
}
```

```javascript
function buildDiamondRepeat(n) {
	let ret = "";
	let i;
  	//i는 0부터 n보다 작을 때 까지 1씩 증가하며 반복
	for(i = 0; i < n; i++){
      	//" "을 n-1만큼 반복하고 "*"을 i만큼 반복하여 ret에 답는다
		ret += " ".repeat(n-i)+"* ".repeat(i)+"\n";
	}
    //i는 n부터 0보다 클 때까지(=1일 때까지) 1씩 감소하며 반복
	for(i; i > 0; i--){
        //" "을 n-1만큼 반복하고 "*"을 i만큼 반복하여 ret에 담는다
		ret += " ".repeat(n-i)+"* ".repeat(i)+ "\n";
	}
	console.log(ret);
	return ret;	
}
```



### 문제 11

두 수를 입력받아서, 두 수의 최대공약수를 반환하는 함수를 작성하세요. ([유클리드 호제법](https://ko.wikipedia.org/wiki/%EC%9C%A0%ED%81%B4%EB%A6%AC%EB%93%9C_%ED%98%B8%EC%A0%9C%EB%B2%95)을 참고하세요.)

```javascript
function gcd(p, q) {
	if(q === 0) return p;
	return q ? gcd(q, p%q) : p;
}
```



### 문제 12

세 수를 입력받아 큰 것부터 차례대로 출력하는 함수를 작성하세요.

```javascript
function sortNumber(n1, n2, n3) {
	const arr = [n1, n2, n3];
	arr.sort().reverse();
	for(let item of arr){
		console.log(item);	
	}
}

function sort(x, y, z){
  //x가 y보다 작으면 x를 temp변수에 넣고 x에는 y값을 넣고 y에는 더 작은 temp값을 넣어준다.
  if(x < y){
    const temp = x;
    x = y;
    y = temp;
  }
  //y가 z보다 작으면 y를 temp변수에 넣고 y에는 z값을 넣고 z에는 더 작은 temp값을 넣어준다.
  if(y < z){
    const temp = y;
    y = z;
    z = temp;
  }
  //x가 y보다 작으면 x를 temp변수에 넣고 x에는 y값을 넣고 y에는 더 작은 temp값을 넣어준다.
  if(x < y){
    const temp = x;
    x = y;
    y = temp;
  }
  console.log(x, y, z);
}
```



### 문제 13

자연수 `n`을 입력받아, `n`번째 피보나치 수를 반환하는 함수를 작성하세요.

```javascript
function fib(n){
  //2보다 작은 수의 피보나치는 자기 자신을 반환한다. 0, 1
  if (n < 2)
     return n;
  else//피보나치 수열에서 n-1번째의 합과 n-2번째의 합이 n번째 피보나치 수를 의미하므로 피보나치의 n-1번째 값과 n-2번째 값을 더하여 반환한다.
     return fib(n-1) + fib(n-2);
}

function fib(n){
  let n2=0; //0번째 피보나치 수열 값
  let n1=1; //1번째 피보나치 수열 값
  let sum;
  if(n === 0){//0일 때는 0번째 수열 값 반환
    sum = n2;
  }else if(n === 1){//1일 때는 1번째 수열 값 반환
    sum = n1;
  }else{//2부터 n번째까지 1씩 증가하며 반복하여 
     for(let i = 2; i <= n; i++){
      sum = n2+n1; //n-2번째 수열 값과 n-1의 수열 값의 합을 대입
      n2 = n1; //다음 반복을 위해 n-2번째 수열 값에 n-1의 값을 대입
      n1 = sum; //다음 반복을 위해 n-1번째 수열 값에 n-2번째 수열 값과 n-1의 수열 값의 합을 대입
    } 
  }
  console.log("n="+sum);
}
```



### FIzzBuzz

```javascript
function fizzBuzz(){
  //1부터 100까지 1씩 증가하며 반복하면서
  for(let i=1; i < 101; i++){
    //3과 5의 배수일 때는 "FizzBuzz"를 출력
    if(i%3 === 0 && i%5 === 0)
      console.log("FizzBuzz");
    //3의 배수일 때는 "Fizz"를 출력
    else if(i%3 === 0)
      console.log("Fizz");
    //5의 배수일 때는"Buzz"를 출력
    else if(i%5 === 0)
      console.log("Buzz");
    //그 외의 수는 숫자를 출력
    else
      console.log(i);
  }
}
```

------

## Array 문제

### 문제 1

두 정수 `start`, `end`를 입력받아, `start`부터 `end`까지의 모든 정수를 배열로 반환하는 함수를 작성하세요.

예:

```
range(3, 6); -> [3, 4, 5, 6]
```

```javascript
function range(start, end){
  const arr = [];
  for(let i = start; i <= end; i++)
  {
    arr.push(i);
  }
  return arr;
}
```



### 문제 2

수 타입의 값으로만 이루어진 배열을 입력받아, 그 값들의 합을 구하는 함수를 작성하세요.

```javascript
function sumArr(numArr){
  let sum = 0;
  for(let num of numArr){
    sum += num;
  }
  return sum;
}
```



### 문제 3

배열을 입력받아, falsy인 요소가 제거된 새 배열을 반환하는 함수를 작성하세요.

```javascript
function filterFalsy(arr){
    const filterArr = arr.filter(returnTruthy);
 	return filterArr;
}

function returnTruthy(value){
  if(!value)
    return false;
  else
    return true;
}

function filter(arr){
  const newArr = [];
  for (let item of arr){
    if(item){
      newArr.push(item);
    }
  }
  return newArr;
}
```

------

## Quiz

1. 다음 실행문의 출력 결과가 무엇인지 선택하세요.

   ```javascript;
   const arr = [1, 2, 3, 4, 5];
   arr.splice(2, 4);
   console.log(arr);
   ```

   1. [1, 2, 3, 4, 5]
   2. [2, 4]
   3. **[1, 2]**
   4. [2, 3, 4, 5]

2. 짝수와 홀수를 판단하여 반환하는 함수의 반환 부분을 완성하세요.

   ```javascript
   function isEvenOrOdd(n) {
   	return (ⓐ === ⓑ)?"짝수":"ⓒ";
   }
   ```

   ⓐ **n%2**, ⓑ **0**, ⓒ **홀수**

3. 다음 실행문의 출력 결과가 무엇인지 선택하세요.

   ```javascript
   const animals = ['ant', 'bison', 'camel', 'duck', 'elephant'];
   console.log(animals.slice(2));
   ```

   1. **["camel", "duck", "elephant"]**
   2. ["duck", "elephant"]
   3. ["ant", "bison", "camel"]
   4. ["ant", "bison", "duck", "elephant"]

4. falsy 값인것을 모두 고르세요. **(모두 선택)**

   1. false
   2. null
   3. undefined
   4. NaN
   5. ""

5. buildDiamondRepeat(5); 를 실행시켰을 때 다음의 결과가 나오도록 for의 조건 부분에 들어갈 값을 선택하세요.

```
    * 
   * * 
  * * * 
 * * * * 
   * * 
  * * * 
 * * * * 
```

```javascript
function buildDiamondRepeat(n) {
	let ret = "";
	let i;
	for(i = 0; i < n; i++){
		ret += " ".repeat(n-i)+"* ".repeat(i)+"\n";
	}
	for(i=ⓐ; ⓑ; ⓒ){
		ret += " ".repeat(n-i)+"* ".repeat(i)+ "\n";
	}
	console.log(ret);
}
```

1. **ⓐ Math.floor(n/2) ⓑ i<n ⓒ i++**
2. ⓐ n ⓑ i<n ⓒ ++i
3. ⓐ n ⓑ i>n ⓒ i++
4. ⓐ Math.round(n/2) ⓑ i<n ⓒ i++