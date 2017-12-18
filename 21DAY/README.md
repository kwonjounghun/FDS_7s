# String 연습 문제
>[패스트캠퍼스 JavaScript 파트 퀴즈 Github](https://github.com/fds7/js-exercise)

## # 문제 5
문자열을 입력받아 그 문자열이 회문(palindrome) 인지 판별하는 함수를 작성하세요.(회문이란, '토마토', 'never odd or even'과 같이 뒤에서부터 읽어도 똑같이 읽히는 문자열을 말합니다.)

```js
// 내풀이
function palindrome(str){
  let before = [];
  let after = [];
  for(let i = 0; i < str.length; i++){
      before.push(str[i]);
  }
  for(let j = str.length - 1; j >=0; j--){
      after.push(str[j])
  }
  for(let k = 0; k < str.length; k++){
      return before[k] === after[k] ? true : false;
  }
}

// 선생님풀이 1. Best
function isPalindrome1(str) {
  for (let i = 0; i < Math.floor(str.length / 2); i++) {
    if (str[i] !== str[str.length - 1 - i]) {
      return false;
    }
  }
  return true;
}

// 선생님풀이 2. 배열메소드 활용
function isPalindrome2(str) {
  const arr1 = Array.from(str);
  const arr2 = Array.from(str).reverse();
  for(let i = 0; i < arr1.length; i++){
      if(arr1[i] !== arr2[i]){
          return false;
      }
  }
  return true;
}

// 선생님풀이 3. 공백문자까지 고려
function isPalindrome3(str) {
  let trimed = Array.from(str.replace(" ", ""));
  let ori = Array.from(trimed).join("");
  let rev = Array.from(trimed).reverse().join("");

  return (ori === rev) ? true : false;
}
```
### 선생님풀이 1. Best
* 문자열을 반으로 나눠, 맨앞과 맨뒤에서부터 비교해보다가 다른 문자가 나오면 바로 루프를 종료한다 -> 반복문 도는 횟수를 줄일 수 있음
* 정확히 중간에 있는 문자는 검사할 필요없다. 회문인지 아닌지에 영향을 미치지 않음
* 문자열도 index로 접근가능하기 때문에, 문자열 비교를 위해 굳이 배열로 만들지 않아도 된다.

* 배열은 객체이다. object형의 자료형은 내용이 같아도 별개의 **통**이기 때문에 다른 값이다
* Array.from 정적 메소드를 통해 문자열을 배열로 쉽게 변환할 수 있다

-----

## # 문제 6

문자열을 입력받아, 그 문자열의 모든 '부분 문자열'로 이루어진 배열을 반환하는 함수를 작성하세요.
```
subString('햄버거');
// 결과: ['햄', '햄버', '햄버거', '버', '버거', '거']
```
```js
function subString(str) {
  let arr = [];
  for (var i = 0; i < str.length; i++) {
    for (var j = i + 1; j <= str.length; j++) {
      arr.push(str.slice(i, j));
    }
  }
  return arr;
}
console.log(subString('햄버거')); //['햄', '햄버', '햄버거', '버', '버거', '거']
```

-----

## # 문제 7

문자열을 입력받아, 해당 문자열에서 중복된 문자가 제거된 새로운 문자열을 반환하는 함수를 작성하세요.

예: `removeDuplicates('tomato'); -> 'toma'`

```js
// 내풀이
function removeDuplicates(str) {
  let sum = '';
  for (let i = 0; i < str.length; i++) {
    sum.includes(str[i]) ? '' : sum += str[i];
  }
  return sum;
}

// 선생님 풀이
function removeDuplicates(str){
    let newStr = '';
    for(let c of str){
        if(!newStr.includes(c)){
            newStr += c;
        }
    }
    return newStr;
}

console.log(removeDuplicates('tomato'));
```
* 조건없이 배열의 맨앞부터 끝까지 다 순회할땐 for...of를 사용하는게 깔끔하다

-----

## # 문제 8
이메일 주소를 입력받아, 아이디 부분을 별표(`*`)로 가린 새 문자열을 반환하는 함수를 작성하세요.

```js
// 내풀이
function secret(email){
    let arr = email.split('@');
    arr[0] = '*'.repeat(arr[0].length);
    let newEmail = arr[0] + '@' + arr[1];
    //let newEmail = arr.join('@');
    return newEmail;
}

// 1. 선생님 풀이
function hideId(email){
    const arr = email.split('@');
    return '*'.repeat(arr[0].length) + '@' + arr[1];
}

// 2. 선생님 풀이 _ 2개의 변수를 동시 선언하여 가독성 GOOD
function hideId2(email){
    const [id, domain] = email.split('@');
    return '*'.repeat(id.length) + '@' + domain;
}
```

-----

## # 문제 9
문자열을 입력받아, 대문자는 소문자로, 소문자는 대문자로 바꾼 결과를 반환하는 함수를 작성하세요.

```js
function changeStr(str){
    let newStr = '';
    for(let c of str){
        c.toLowerCase() === c ? newStr += c.toUpperCase() : newStr += c.toLowerCase();
    }
    return newStr;
}

console.log(changeStr('HiHiBongBong'));
```
* toUpperCase(), toLowerCase()메소드는 원본문자열을 바꾸지않는다

-----

## # 문제 10
문자열을 입력받아, 각 단어의 첫 글자를 대문자로 바꾼 결과를 반환하는 함수를 작성하세요. (문자열에 개행이 없다고 가정합니다.)

```js
//내풀이
function capital(str){
    let arr = str.split(' ');
    let newStr = '';
    console.log(arr);
    for(let word of arr){
        newStr += word[0].toUpperCase() + word.slice(1) + ' ';
    }
    return newStr;
}
console.log(capital('hey pretty bong!')); //Hey Pretty Bong


//선생님풀이
function capitalize(str) {
  let newStr = '';
  for (let i = 0; i < str.length; i++) {
    if (str[i - 1] === ' ' || i === 0) {
      newStr += str[i].toUpperCase();
    } else {
      newStr += str[i];
    }
  }
  return newStr;
}
```
* 혹시라도 공백이 여러개 들어가있을수도 있는 경우까지 대비

-----

## # 문제 11

문자열을 입력받아, 문자열 안에 들어있는 단어 중 가장 긴 단어를 반환하는 함수를 작성하세요. (문자열에 개행이 없다고 가정합니다.)

```js
// 내풀이
function longWord(str) {
  let arr = str.split(' ');
  let result = '';

  for (let i = 0; i < arr.length; i++) {
    if (arr[i].length > result.length) {
      result = arr[i];
    }
  }
  return result;
}
console.log(longWord('hey hi hello')); //hello

// 선생님 풀이
function longestWord(str){
    const arr = str.split(' ');
    let longest = arr[0];
    for(let i = 1; i < arr.length; i++){
        if(arr[i].length > longest.length){
            longest = arr[i];
        }
    }
    return longest;
}
```
* 이경우엔 split(' ')해서 공백이 배열의 원소로 생겨도 가장 긴 문자열이 될 확률이 없으니, 안심하고 사용해도 된다.

-----

## # 문제 12
문자열 `s`과 자연수 `n`을 입력받아, `s`의 첫 `n`개의 문자만으로 이루어진 새 문자열을 반환하는 함수를 작성하세요.

```js
// 내풀이
function changeStr(s, n){
    let newStr = '';
    for(let i = 0; i < n; i++){
        newStr += s[i];
    }
    return newStr;
}

console.log(changeStr('Hello', 4));

// 선생님 풀이
function changeStr(s, n){
    let newStr = '';
    for(let i = 0; i < n && i < s.length; i++){
        newStr += s[i];
    }
    return newStr;
}
```

* 문자열길이보다 큰 자연수를 넣으면 undefined가 뜨는 에러가 생길 수 있다  
=> 안전장치 `i < n && i < s.length;`를 넣어준다

-----
# Math 연습문제

## # 문제 5
임의의 HTML 색상 코드를 반환하는 함수를 작성하세요.

```js
// 내풀이
function colorPicker() {
  let color = '#';
  let code = '123456789abcdef'
  for (let i = 0; i < 6; i++) {
    let num = Math.floor(Math.random() * 15);
    color += code[num];
  }
  return color;
}

// 16진수의 성질을 이용한 풀이
function randomHtmlColor2(){
    const value = Math.random() * 256 * 256 * 256;
    return '#' +
    // 버그없는 방법 찾아보기
}
```
-----

## # 문제 6
양수를 입력받아, 그 수만큼의 길이를 갖는 임의의 문자열을 반환하는 함수를 작성하세요.
```js
function randomStr(n) {
  let newStr = '';
  for (let i = 0; i < n; i++) {
    const randomIndex = Math.floor(Math.random() * str.length);
    newStr += str[randomIndex];
  }
  return newStr;
}
```
