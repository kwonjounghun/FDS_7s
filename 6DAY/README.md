# **로그인 영역 마크업**
```html
<form action="javascript:alert('hi');" class="login-form">
<fieldset>
    <legend>회원 로그인 폼</legend>
    <div class="user-email">
    <label for="user-email">아이디</label>
    <input type="email" id="user-email" placeholder="ID or Email" required>
    </div>
    <div class="user-pw">
    <label for="user-pw">비밀번호</label>
    <input type="password" id="user-pw" placeholder="8자리 이상" required>
    </div>
    <button type="submit" class="btn-login">로그인</button>
</fieldset>
</form>
```         
## # form태그
HTML폼은 사용자에게 데이터를 물어보고 웹서버로 데이터를 전달하는 데 편리한 방법이다. action, method속성으로 데이터를 어디에 어떻게 보낼지 설정할 수 있다. 
>기본구조: form > fieldset > legend
* HTML 4.0 에선 form 에 fieldset legend 필수아님
* XHTML 1.0 에선 form 에 fieldset legend 필수 (엄격함) 
* HTML5는 이 두 문법을 허용함
### 1. 서버와 통신이 필요한 경우엔 `<div>`태그가 아닌 `<form>`태그로 마크업!
* div태그로 쓰고 javascript로 서버통신을 제어하는 것은 좋지 않은 방법이다   
ex) 기본기술이 없는 환경이 있을 수 있음. 후진국이나 모바일에서 자바스크립트를 사용할 수 없거나 네트워크가 매우 좋지 않으면 페이지의 기본 기능을 사용할 수 없게 된다.
### 2. fieldset
독립된 개요(아웃라인)를 생성. 연관성있는 컨트롤을 묶을 때 div 혹은 fieldset 묶어주면 된다.
### 3. legend
그룹의 이름으로 사용되는 태그
-----
## # input요소는 반드시 1대1로 대응되는 id와 label을 가져야한다
label이 보이지 않아도 접근성을 위해마크업 해주도록 한다
1. label을 .readable-hidden으로 -> BEST!
2. label은 생략하고, input태그에 title속성으로 보충설명 해도되긴함 (한국에서만 허용. W3C에선 허용안함)
### 1. placeholder
입력란에 들어가야할 내용 힌트를 주는 속성
### 2. title
상황에따라 부연설명이 필요하면 주도록한다. placeholder에 충분히 설명 되어있는데, 같은내용을 중복해 쓰지말도록
-> 네이버 로그인 openwax 점수안좋은 예
* IE7에서 alt를 title처럼 툴팁으로 제공하는 버그가 있었음
-----
# **로그인 영역 CSS**
## # CSS3에 추가된 색상속성 rgba, hsla
* hsla: 인간이 색상을 추출하기 가장 좋은 방식
    * hue 0~360
    * saturation 0~100
    * lightness 0~100
    * alpha 0~1
* rgba (red, green, blue, alpha)
## # CSS선택자과 구체성점수
요즘 id선택자느 되도록 안쓰는 추세이다. 구체성점수 큰게 들어오는 순간 경우의 수가 그많큼 많아지기 때문.   
-> 구체성 점수가 낮은 태그선택자, 속성선택자를 사용하도록!
```css
input [type="email"]{
    background: pink;
}
```
다양한 타입의 input상자(radio, checkbox등)을 개별선택할 수 있다. 이걸 몰랐으면 마크업에 class를 일일히 사용해 마크업이 길졌을지도 모른다.
## # button 디자인
버튼이 유독 브라우저별 user-agent스타일이 다르다 -> .btn이라는 공통클라스를 만들고 디자인을 모듈화 하도록 하자
* 버튼을 디자인 할때는 반드시 padding과 margin을 재설정해준다
* 리셋코드에 button태그도 추가해준다
-----
# 유효성 검사 배너  
## HTML 구조  
```html
<div class="validation">
          <h2 class="validation-heading readable-hidden">유효성 검사 배너 링크</h2>
          <ul class="validation-list">
            <li><a href="https://validator.w3.org/#validate_by_upload" title="마크업 유효성검사 사이트로 이동 새창" target="_blank">W3C Markup Validation</a></li>
            <li><a href="https://jigsaw.w3.org/css-validator/#validate_by_upload" title="CSS 유효성검사 사이트로 이동 새창" target="_blank">CSS Validation Service</a></li>
          </ul>
        </div>
```  
title : 보충 설명.  
target="_blank" : URL을 새 창으로 실행.  

## CSS 구조  
```css
.validation {
  margin-top: 20px;
}
.validation-list a {
  border: 1px solid #aaa;
  display: block;
  margin-bottom: 10px;
  height: 35;
  line-height: 20px;
  border-radius: 20px;
  padding-left: 45px;
  padding-bottom: 5px;
  background: url("./images/validation_icon.png") no-repeat 15px 50%, linear-gradient(to bottom, #ccc, #eee);
}
```  
1.로그인 폼과 유효성 검사 배너 링크 20px 거리를 유지하기 위해 .validation에 margin-top으로 20px를 적용한다.  
2.배너 상자 모두가 링크로 사용될수 있도록 .validation-list a를 상자로 사용한다.  
3.상자의 크기를 조정하고, line-height와 padding-left를 사용하여 글을 가운데로 움직인다.  
4.그림은 먼저 적용한 것이 위로 오기 때문에, 위에 올 이미지 파일을 url로 불러오고 no-repeat로 반복하지 않으며 x축과 y축을 조정한다.  
5.밑에올 배경색을 linear-gradient사용해서 위에서 아래로 #ccc색에서 #eee색으로 배경을 지정한다.  

# 웹 관련 용어  
## HTML 구조  
```html
<div class="term">
    <h2 class="term-hadding">웹 관련 용어</h2>
    <dl class="term-list clearfix">
        <dt class="term-list-heading">웹 표준 이란?</dt>
        <dd class="term-list-thumbnail"><img src="./images/web_standards.gif" alt="W3C 로고"></dd>
        <dd class="term-list-brief">W3C 단체에서 규정한 웹 기술 사양에 대한 규칙을 말하며 표준 규격은...</dd>
    </dl>
</div>
```  
### dl Tag   
dt(용어 제목), dd(용어 설명) 태그를 가질 수 있다.  
dt와 dd는 1:1대응, 1:n대응, n:n대응이 가능하다.  

## CSS 구조    
```css
.term {
  background: linear-gradient(to bottom, #eee, #ccc);
  border: 1px solid #aaa;
  border-radius: 5px;
  padding: 10px 15px;
  margin-top: 20px;
}
.term-heading {
  font-family: "Noto Sans Bold";
  font-size: 1.5rem;
  font-weight: bold;
}
.term-list {
  margin-top: 10px;
}
.term-list-heading {
  font-weight: bold;
  width: 145px;
  float: right;
  color: #296897;
}
.term-list-thumbnail {
  width: 60px;
  float: left;
}
.term-list-brief {
  width: 145px;
  float: right;
  margin-top: 5px;
}
``` 
### float와 inline 사용법.  
1.term-list-thumbnail에 float:left한다.  
>//term-list-heading가 블록요소 이므로, term-list-thumbnail에 영역을 제외한 나머지 영역에만 글이 출력된다.  

2.term-list-heading과 term-list-brief를 inline-block으로 만든다.  
>//inline-block이 되면서 정해진 width없이 부모 영역만큼 글이 출력된다.   

3.term-list-thumbnail에 margin-right를 주어 term-list-heading과 term-list-brief와 거리를 둘수 있다.    
>//term-list-heading과 term-list-brief에 margin을 줄 필요가 있을 경우 문제가 된다.    

### float에 left와 right 사용.  
1.term-list-heading + term-list-thumbnail 또는 term-list-brief + term-list-thumbnail가 부모 영역보다 작은 값을 설정한다.

2.term-list-heading, term-list-brief는 float:right 하고 term-list-thumbnail는 float:left한다.

------



