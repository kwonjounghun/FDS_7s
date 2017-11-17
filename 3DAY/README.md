# FDS 7기 강의 내용 정리(2017년 11월 15일)

## 마크업의 첫 번째 순서는 '구조설계'이다
> .header 영역 안에 로고/텍스트링크/메뉴, **논리적(구성)순서** 결정

```html
<header class="header">
    <h1 class="logo">
        <a href="#"><img src="images/logo.png" alt="Web Cafe"></a>
    </h1>
    <ul class="member">
        <li><a href="#">홈</a></li>
        <li><a href="#">로그인</a></li>
        <li><a href="#">회원가입</a></li>
        <li><a href="#">사이트맵</a></li>
        <li><a href="#"><em>english</em></a></li>
    </ul>
    <nav class="navigation">
        <h2 class="readable-hidden">메인메뉴</h2>
        <ul class="main-menu">
        <li tabindex="0" >
            <span>HTML에 대해</span>
            <ul class="sub-menu about-html">
            <li><a href="#">HTML5 소개</a></li>
            <li><a href="#">레퍼런스 소개</a></li>
            <li><a href="#">활용 예제</a></li>
            </ul>
        </li>
        <li tabindex="0">
            <span>CSS에 대해</span>
            <ul class="sub-menu about-css">
            <li><a href="#">CSS 소개</a></li>
            <li><a href="#">CSS2 VS CSS3</a></li>
            <li><a href="#">CSS 애니메이션</a></li>
            <li><a href="#">CSS 프레임워크</a></li>
            </ul>
        </li>
            <li tabindex="0">
            <span>웹표준</span>
            <ul class="sub-menu web-standards">
            <li><a href="#">웹표준이란?</a></li>
            <li><a href="#">W3C</a></li>
            <li><a href="#">HTML의 현재와 미래</a></li>
            </ul>
        </li>
        <li tabindex="0">
            <span>웹접근성</span>
            <ul class="sub-menu web-accessibility">
            <li><a href="#">웹접근성의 개요</a></li>
            <li><a href="#">장애환경의 이해</a></li>
            <li><a href="#">장차법</a></li>
            <li><a href="#">웹접근성 품질마크</a></li>
            </ul>
        </li>
        <li tabindex="0">
            <span>묻고답하기</span>
            <ul class="sub-menu qna">
            <li><a href="#">묻고답하기</a></li>
            <li><a href="#">FAQ</a></li>
            <li><a href="#">1대1 질문</a></li>
            <li><a href="#">웹표준</a></li>
            <li><a href="#">웹접근성</a></li>
            </ul>
        </li>
        <li tabindex="0">
            <span>자료실</span>
            <ul class="sub-menu archive">
            <li><a href="#">공개 자료실</a></li>
            <li><a href="#">이미지 자료실</a></li>
            <li><a href="#">웹표준 자료실</a></li>
            <li><a href="#">웹접근성 자료실</a></li>
            </ul>
        </li>
        </ul>
    </nav>
    </header>
````


### 1. 로고

```html
<h1 class="logo">
    <a href="#"><img src="images/logo.png" alt="Web Cafe"></a>
</h1>
```

> 이미지가 읽히지 않을 때(예를 들어, 네트워크가 원활하지 않을 때) 대체되는 텍스트
>> 의미있게 작성되어야 하며, 스크린리더기가 제대로 읽기 위해 적당한 띄어쓰기가 필요함

> 이미지에 대한 대체텍스트의 중요성 고려 
>> 브라우저에서 headingsmap을 이용하여 자료구조를 확인 할 때 제목이 비어있어 파악하기 힘듦


### 2. 대체텍스트 text link
```html
<ul class="member">
    <li><a href="#">홈</a></li>
    <li><a href="#">로그인</a></li>
    <li><a href="#">회원가입</a></li>
    <li><a href="#">사이트맵</a></li>
    <li><a href="#"><em>english</em></a></li>
</ul>
```

> ol(ordered list), 순서가 있는 리스트 | ul(unordered list), 순서와 상관없이 나열되는 리스트 - 컨텐츠의 종류에 따라 선택

(위의 텍스트 링크 마크업 참고)
로그인/회원가입을 해야만 사이트로서 사용이 용이할 때(서비스관점), 주메뉴보다 우선일 수 있다.
또한, 사용자의 관점 혹은 서비스 관점에서 우선순위는 바뀔 수 있다.


### 3. 로그인
> 문서안에 문서를 품은 형태를 iframe
예) 다음/네이버 로그인, 로그인 버튼 전에 로그인유지 체크박스 마크업이 되어야 함

> 디자인에 종속된 마크업을 하면 안됨, 논리적 흐름에 따라 의미있는 마크업을!
이미지/텍스트로 처리 하는데 고민해볼 것 결정은 개발자의 몫..


### 4. `<a>` 태그
변경된 약관(<<여기에 링크연결)


### 5. 숨김 헤딩 처리(스크린리더기가 해당컨텐츠를 인식하기 위한)


### 6. 그룹핑(묶음)
- div, span - 중립적 요소, 그룹핑한다.
    - div 블록요소
    - span 인라인요소
```html
<span>HTML에 대해</span>
```
여기서, 텍스트를 선택하기 위해 span사용


### 7. CSS
- CSS file
    - .css 개발버전 - 주석 및 단락포함
    - .min.css 배포버전 - 최적화됨

- CSS workflow
    - 개발버전 - uglify - 미니멀라이즈 - 배포 순서로 진행


### 8. 벤더프리픽스 - 브라우저별 접두사

-webkit- 크롬, 사파리, 인터넷
특정 브라우저 사에서만 제어하기 위한 접두사

### 9. normalize.css
- normalize.css를 통해 agent style(각 브라우저가 기본적으로 가지고 있는 속성)을 재설정
- 각 브라우저별 동일하게 설정

### 10. cascading(겹침)
- 마진병합현상

### 11. reset.css / 에릭마이어
- *(모두)선택해서 리셋하는 방법보다 필요한 태그만 추려 리셋설정 하는 것이 성능 면에서 좋음
- 필요하지 않은 요소설정을 피할 수 있기 때문에..

- font:inherit; 강제상속값

- 구형버전 브라우저에선 정의되지 않은 요소(html5속성)을 인라인속성으로 인식
    - display:block;으로 재설정

```css
table {
    border-collapse: collapse;
    border-spacing: 0;
}
```

- border-collapse: collapse;
    - 테이블 th, td에 border를 보여줄 때 border-collapse: collapse를 사용하여 겹치는 선을 하나로 보이도록 설정


-  CSS선언순서의 중요성
    - 최후의 CSS file 또는 line이 렌더링되며 가장 나중에 선언된 CSS로 덮어쓴다

### 12. 웹폰트
- @font-face 폰트의 자원과 성격을 선언
- 이와 같은 선언은, 폰트를 선 다운로드 후 적용되며, 폰트용량 커질수록 성능상 부담

- 폰트형태
    - serif 삐침이 있음 예, 바탕체
    - sans-serif 반듯한 고딕계열

- 다양한 폰트를 선언해서 만약 해당폰트가 존재하지 않을 때 차선책으로 적용할 대안 제시해야 함
- CSS Validation Service는 @import 또는 @font-face(웹폰트) 체크는 불가

- 폴리필(호환성)
    - 지원하지 않은 간극을 스크립트가 지원
    - 완벽하진 않으나 호환시킬 수 있다. 단, 성능이 느려질 수 있음

- Noto sans/ Spoka sans/ 본고딕 : 다 같은 폰트. 용량 큼.
    - 참고  | (링크) https://www.slideshare.net/wsconf/web-font-wsconfseoul2017-vol2
김원준 - 웹폰트(Web Font) 파헤치기 [WSConf.Seoul.2017. Vol.2]
    - 로컬경로 우선설정
    - 오페라는 이제 웹킷계열 렌더링엔진으로 포함됨
    - 성능에 최적화된 순서로 정해진 최종본 (슬라이드50p)
    - woff2 최신지원브라우저 먼저 선언필요, 이후 woff선언

### 13. 병합/상속/구체성 이슈
- margin collapsing(마진병합)
    - margin은 투명한 영역으로 병합이 발생(겹침이슈)
    - cf. padding은 병합되지 않음

- 상속이슈
    - a링크 color(agent기본속성)은 blue
    - 내가 설정한 값이 기본속성의 값보다 우선순위가 높다
    - 배치/레이아웃은 상속되지 않음
    - 데코레이션 속성은 상속되는 경향이 많음

- 구체성 이슈 - 선언순서 중요
    - a:link, a:visited(먼저 선언되어야 함)
    - a:hover, a:focus 

### 14. position
- fixed : viewport기준으로 배치됨
- relative: 자기자신을 기준으로 배치, 본래 있었던 위치 기준으로 이동

### 15. 모바일 링크 혹은 버튼 클릭 시 영역사이즈
- 성인남성 검지손가락 기준, 화면을 클릭하는 영역은 최소 44px 

### 16. css는 인덱스를 1부터 시작
- nth-child(2) : 2번째 요소
- nth-child(n+6) : 6번째부터 나머지 전부요소 선택


# 실습
```css
@charset "utf-8"; /*인코딩선언*/
@import url("./normalize.css"); /*파일을 가져옴*/
@import url("./fonts.css");
*, *::before, *::after{
    box-sizing: border-box; /* ie8 지원 MS*/
}
```
> box-sizing속성은 ie8부터 지원


```css
/* 본문스타일 */
html {
    font-size: 10px;
}
body {
    font-family: 'Noto Sans Regular', sans-serif;
    font-size:1.4rem;
    color:#181818;
}
```
- 루트 요소 html에 고정 폰트 사이즈를 지정
- 최상위 요소인 html요소의 font-size에 비례하니까 1.4배인 14px로 보임, rem(root equal M)
- 0.825em = 14px,  픽셀은 고정값. em(equal M)은 유동적인값(user agent값을 이용하고 싶다면 em을 써야함)

```css
/* 링크스타일 */
a:link, a:visited {
    color:inherit;
    text-decoration: none;
}
a:hover, a:focus {
    color:#f00;
}
```
- 상속값을 준 상위부모로 값을 찾아 올라간다

```css
/* 공통스타일*/
.clearfix::after {
   content: "" ;
    display: block;
    clear: both;
}
```
- 기본적으로 가상요소는 display:inline
-  content: "" 글자 한줄의 높이만큼 영역이 잡힘

```css
/* 헤더 */
.header {
    background-color: #fff;
    position: relative;
    padding:0 30px 30px;
    border-radius:0 0 15px 15px;
}
/* 로고 */
.logo {
    position: absolute; /*블록요소가 되며 레이어로 떠있는 상태로 변화*/
    top:48px;
    left:65px; /*offset조정*/
}
/* 멤버링크 */
.member {
    text-transform: uppercase;
    font-size:0; /*부모요소에 글자사이즈0*/
    text-align:right;
    transform: translateX(10px); 
}
```
- transform: translateX(10px) : x축으로 이동. position과 offset을 이용한 클래식방법보다 애니메이션 속성이 성능이 좋다

```css
.member li{
    display:inline-block; /*ie8이상지원*/
    font-size:1.4rem;/*해당콘텐츠 글자크기 재정의*/
    padding:10px 0;
}
```
- 로고를 배치하기 위해 position:absolute값을 줬고 top, left를 이용해 위치(offset)을 조정
- .header영역에 position:relative 주어 .logo가 .container영역 밖으로 튀어나가지 않도록 함
- position:relative는 자기 자신을 기준으로 자식들을 배치하기 때문에 로고가 .header영역 기준으로 offset이 위치
- .member의 li를 가로로 배치하기 위해 display:inline-block을 사용(inline-block값은 ie8부터 지원)

```html
<ul class="member">
    <li><a href="#">홈</a></li>
    <li><a href="#">로그인</a></li>
    <li><a href="#">회원가입</a></li>
    <li><a href="#">사이트맵</a></li>
    <li><a href="#"><em>english</em></a></li>
</ul>
```

- .member의 li에 인라인 요소인 a가 존재하고 그 안에 텍스트가 존재하므로 그만큼의 영역만큼 블록영역이 잡힘. 단, 마크업 구조 때문에 반각(간극)이 생기고, 이를 해결하기 위해 부모요소 .member에 font-size:0;을 주어 사이 간격을 없앰

- 부모요소인 .member의 font-size가 상속되어 자식인 .member li 안에 텍스트가 보이지 않으므로, .member li에 font-size를 재정의하여 텍스트를 키움

### float.html 
0. float을 clear하는 방법에 따라 다양한 css를 작성

1. float을 준 부모요소에 overflow:hidden 사용
- 넘치는 영역을 계산하는 방식(가로세로 영역체크)에서 자식요소의 사이즈 책정하여 영역을 잡음
- 자식요소인 이미지와 텍스트 중 이미지가 넘치지 않을 만큼 영역을 잡는데 육안으로는 별다른 차이가 없음
2. float은 block요소에만 적용가능(inline상태는 불가능), float이 되는 순간 이미지의 높이만큼의 영역이 소멸, 즉 이미지가 float되며 이미지가 가지고 있던 높이영역을 잃는다

```css
.box1 {
    background: gold;
    overflow: hidden; 
}
.box1 img {
    float:left; 
}
.box1::after {
    content:""; 
    display:block;
    clear:both;
}
.clx {
    clear:both
}
.box2 {
    background: pink;
    display: block;
}
```

3. 가상선택자(::after) 사용하여 clear
content:””;으로 가상의 인라인태그를 만들고 블록속성으로 변경(display:block) 후 clear:both
4. 클래스를 이용하여 clear
.clx 클래스를 만들어 clear:both를 적용. HTML 마크업 .box1영역 안쪽 마지막에 div.clx 부여