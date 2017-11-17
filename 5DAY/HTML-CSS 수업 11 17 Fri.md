# 11 17 Fri
## 쌤 컴퓨터 고장으로 잠깐 머시기
* seulbi.github.io 마크업 구조 생각해보기.
* 마크업 구조 짜보는 연습을 많이 하는 것이 좋다.
* 코딩을 바로 하지 말고 ‘그림 그리는’ 시간을 많이 가져보자!
* 주말에 반응형 기능까지 생각해서 마크업 해보자.
- - - -
#### 숨김 메뉴
* menu-act 동적 핸들링
* 코드를 알고 있는 것 보다 어떤 동작을 원하는 지 명확히 하는 것이 중요하다.
#### jQuery 살짝 
```
<head>
  <meta charset="UTF-8">
  <title>웹카페 - HTML, CSS3, 웹접근성</title>
  <link rel="stylesheet" href="css/style.css">
  <script src="js/jquery.js"></script>
  <script src="js/menu-tab.js"></script>
</head>
```
이렇게 하면 스크립트 때문에 로딩이 길어질 것 같지만,
```
$(document).ready(function() {
  $('.main-menu > li').hover(function() {
    $(this).find('.sub-menu').toggleClass('menu-act');
  });
});
```
* $(document).ready(); <- html 도큐먼트가 모두 로드 된 다음 스크립트 실행하라 이기 때문에 괜찮음
* $(‘.main-menu > li’) <- css랑 같은 방식으로 클래스를 선택할 수 있음
* $(this) <- 선택된 요소(여기서는 .main-menu > li)
```
$(document).ready(function() {
  $('.main-menu > li').hover(function() {
    $(this).find('.sub-menu').toggleClass('menu-act');
  });
  $('.main-menu > li').on('focusin', function() {
    $(this).find('.sub-menu').addClass('menu-act');
  });
  $('.sub-menu li:last-child a').on('focusout', function() {
    $(this).find('.sub-menu').removeClass('menu-act');
  });
});
```
* 위 코드는 Shift-Tab 했을 때 겹침 현상이 일어났었음
```
$(document).ready(function() {
  var menu = $('.main-menu > li');

  menu.hover(function() {
    $(this).find('.sub-menu').toggleClass('menu-act');
  });
  menu.focusin(function() {
    $(this).siblings().find('.sub-menu').removeClass('menu-act');
    $(this).find('.sub-menu').addClass('menu-act');
  });
});
```
이렇게 수정하여 해결
- - - -
### 애니메이션
```
.box {
  width: 100px;
  height: 100px;
  background: lime;
  border: 2px solid #000;
  transition-property: border-radius, background;
  transition-duration: 3s, 2s;
  transition-delay: 0s, 3s;
}
.box:hover {
  border-radius: 50%;
  background: aqua;
}
```
* `transition-property`  <- 트랜지션 효과를 넣을 프로퍼티를 선택
* `transition-duration` <- 트랜지션에 걸리는 시간
* `transition-delay` <- 트랜지션 효과 시작하는 타이밍 시간차 두기
* `transition-timing-function` [linear / ease / ease-in / ease-out / ease-in-out]
[Transition Timing Functions < CSS | The Art of Web](http://www.the-art-of-web.com/css/timing-function/)
[cubic-bezier.com](http://cubic-bezier.com/)
관련 자료 구글링 해보자!
* 역시 단축 표기법이 존재함
예)`transition: border-radius 3s 0s ease-in-out, backround 2s 0s ease-in-out;`
`transition: all 2s ease-in-out;`
- - - -
#### 배경 이미지
* `background-image: url””;`
* `background-repear:;`
* `background-position` 픽셀, 백분율 등을 사용할 수 있음

#### 특수문자 입력
<HTML> <- &ltl HTML $gt;
[HTML Entities](https://www.w3schools.com/html/html_entities.asp)
- - - -
### 애니메이션-2
* 무작정 코딩 말고 어떤 것이 필요할 지 한 번 적어보는 것이 좋다.
예)
	1. 이동 -> translate(x, y)
	2. 글자크기 -> font-size:
	3. 투명도 -> color: rgba();
```
@keyframes text-ani {
  0% {
    font-size: 12px;
  }
  100% {
    font-size: 24px;
  }
}
```
::0% -> from ,100% -> to 와 같은 뜻임::
```
.visual-text {
  background-color: yellow;
  animation-name: text-ani; /* 위에서 선언한 동작명을 호출 */
  animation-duration: 2s;
  animation-fill-mode: forwards;
}
```
* position 값 입력하는 것 보다 translate을 쓰는 것이 성능면에서 좋다(position은 계속 다시 페인팅 함 [Gecko Reflow Visualization - mozilla.org - YouTube](https://www.youtube.com/watch?v=ZTnIxIA5KGw)).
* [배영 - CSS Animation 성능 이론과 실제 적용 사례 WSConf.Seoul.2017. Vol.2](https://www.slideshare.net/wsconf/css-animation-wsconfseoul2017-vol2)
* `animation-iteration-count` <- 재생 횟수
* `animation-direction: alternate;` <- 애니메이션 재생 방향. 여기서는 와리가리 임
* `animation-timing-function` <- 아까 나왔음 
* `animation-play-state: paused;` <- 버튼 요소를 추가하면 플레이 버튼으로 사용할 수 있겠다
* 역시 shorthand 가 있다. `animation: text-ani 2s forwards ease-in-out;`

#### 잠깐) steps 애니메이션
* 지정된 시간에 몇 개의 steps를 넣어서 애니메이션 할 지 지정
* 예)`animation: frame-animation 1s steps(10) infinite;`
* [Steps Animation](https://codepen.io/simurai/pen/tukwj) <- codependent.io 참고 하면 좋다.
* 재밌는 거 많이 만들어 올려서 인기인이 되어보자!

### 가상클래스 애니메이션
* ::before / class / ::after 각각 레이어 순서가 0 1 2 임
```
.visual::before, .visual::after {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}
```
* `content: "";` <- 넣는 것을 잊지 말자
* `animation-delay` <- 설정한 애니메이션 재생 시작 시간차 주기

#### 잠깐)SCSS
CSS 전처리기 컴파일하면 일반 CSS가 됨
- - - -
## Mediaquery
[» CSS3 미디어쿼리 이해 - NARADESIGN](http://naradesign.net/wp/2012/05/30/1823/)
* 반응형 웹을 위한
* mobile-first 전략: 모바일 css를 먼저 구현하는 것이 좋다
* `@media all and (min-width: 가로픽셀) {}` <- 이런 식으루 디바이스 디스플레이의 크기를 기준으로 구분해줌
```
@charset "utf-8";

/* All Device */
                            /* <- 768px 아래 디바이스에 적용됨 */
/* 태블릿 디바이스 이상 */
@media screen and (min-width: 768px) {}
```
* head 태그 안에  `<meta name="viewport" content="width=device-width">` 를 반드시 추가해줘야 함

#### 잠깐) Accesibility 이슈: 전경/배경 명도 대비가 4.5:1 을 넘어야 함
- - - -
## 과제: seulbi.github.io
* 논리적 순서를 고려해서 마크업 해오자
* media query 적용해보자
* flex 말고 다른 것도 해보자
* 자기계정.github.io 에 올리고 주소 제출하자
- - - -
## Form
### 로그인 상자
	1. 로그인 -> H2.login-heading
	2. 아이디 ->
	3. 비밀번호
	4. 버튼
	5. 링크텍스트
::읽어보기::: [CSS방법론 SMACSS, BEM, OOCSSWIT - NTS UIT Blog | WIT - NTS UIT Blog](http://wit.nts-corp.com/2015/04/16/3538)
```
<div class="login">
          <h2 class="login-heading">로그인</h2>
          <form action="[submit 클릭하면 데이터가 입력될 서버]" class="login-form">
            <fieldset>
              <legend>회원 로그인 폼</legend>
              <div class="user-email">
                <label for="user-email">아이디</label><input type="text" id="user-email">
              </div>
              <div class="user-pw">
                <label for="user-pw">비밀번호</label><input type="password" id="user-pw">
              </div>
              <button type="submit" class="btn-login">로그인</button>
            </fieldset>
          </form>
        </div>
```
* form 요소들을 fields 태그로 묶어주고 legend로 정의해줌
*  `<label for="user-pw">비밀번호</label><input type="password" id="user-pw">`
	* label 태그 안의 for=“” 와 input 태그 안의 id=“” 를 연결 시키자  