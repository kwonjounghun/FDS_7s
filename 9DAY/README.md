# Today I Learned

## 2017년 11월 23일

<br />

### 01 WAI-ARIA

#### 1. Tab 컨트롤 제어

```javascript
$(document).ready(function() {
  $('[role="tab"]').on('click', function(e) {
    
    // 선택된 제이쿼리 객체의 기본 동작 실행을 막는다.
    e.preventDefault();
	
    // ‘aria-selected’ 속성을 true로 설정하고 형제 요소의 ‘aria-selected’ 속성을 false로 설정한다.
    $(this).attr('aria-selected', true).siblings().attr('aria-selected', false);
    
    // $(selectedId)에 의해 선택된 객체에 'tablpanel-open' 클래스를 추가하고 형제 요소의 'tablpanel-open' 클래스를 제거한다.
    var selectedId = "#" + $(this).attr('aria-controls');
    $(selectedId).addClass('tabpanel-open').siblings().removeClass('tabpanel-open');
  });
});	
```

##### 1.1 preventDefault()

- 이벤트 발생에 따른 객체의 기본 동작을 막는다.
- `a` 요소가 click 이벤트를 받았을 때의 기본 동작은 href 속성 값에 설정된 url로 이동하는 것이다. 이 때 a 요소가 click 이벤트를 받았을 때 `preventDefault()`가 실행되도록 하면 이 기본 동작은 실행되지 않는다.

##### 1.2 [정보 접근성 향상을 위산 W3C 국제 표준 WAI-ARI 사례집](www.wah.or.kr)

<br />

<br />

<br />

### 02 .event

#### 1. Sprite Image와 IR 기법

##### 1.1 Sprite Image

- 웹 페이지에서 사용하는 이미지가 많아질수록 그만큼 서버에 HTTP 요청 횟수가 증가하고, 이는 결국 렌더링 성능 저하를 가져온다. 이를 해결하기 위한 방법이 바로 **Sprite Image**이다.
- Sprite Image는 여러 개의 개별 이미지 파일을 하나로 합쳐놓은 파일이다.
- 실제 사용할 때는 css의 `background-image`, `background-position` 속성을 사용해 알맞은 부분만 노출한다.

##### 1.2 IR 기법

- IR 기법이란 이미지로 글자를 감추는 기법을 말한다.

- IR 기법과 Sprite Image는 짝꿍처럼 자주 함께 쓰인다.

- IR 기법을 적용하는 방법은 다음과 같다.

  1. 요소의 `height`와 같은 값만큼 `padding-top`을 설정하여 글자를 아래로 미뤄내고 `overflow: hidden`을 이용해 감추는 방법

  2. 가상 클래스에 `background-image`를 적용하고 `position: absolute`를 이용해 글자를 감추는 방법

     ```html
     <!DOCTYPE html>
     <html lang="ko">
     <head>
       <meta charset="UTF-8">
       <title>IR Example</title>
       <style>
         /* 방법 1 */
         h1 {
           background: pink url("images/title.png") no-repeat;
           width: 290px;
           height: 0;
           padding-top: 195px;
           overflow: hidden;
         }

         
         /* 방법 2 */
         h1 {
           width: 290px;
           height: 195px;
           position: relative;
           font-size: 1em;
           padding: 20px;
           box-sizing: border-box;
           background: yellow; 
         }
         
         h1::after {
           content: "";
           position: absolute;
           top: 0;
           left: 0;
           width: 100%;
           height: 100%;
           background: url("images/title.png") no-repeat;
         }
       </style>
     </head>
     <body>
       <h1>Fast Campus</h1>
     </body>
     </html>
     ```

- button 요소에 첫 번째 방법으로 IR 기법을 적용하려 하면 각 브라우저 별로 다른 렌더링 결과를 나타내기 때문에 문제가 된다. 현업에서는 이 문제를 해결하기 위해 `span` 또는 `a` 태그를 사용하지만 이는 더 복잡한 문제를 야기시킨다. 가장 좋은 방법은 **button을 float 처리한 후 button을 그루핑하여 그루핑한 요소에 clearfix 클래스를 추가**하는 것이다.

  ```html
  <!DOCTYPE html>
  <html>
    <head>
      <title>IR Example 2</title>
      <style>
        .btn-event button {
          float: left;
          width: 19px;
          height: 18px;
          padding-top: 18px;
          overflow: hidden;
          background-image: url("images/back_forward.png");
          background-repeat: no-repeat;
        }
      </style>
    </head>
    <body>
      <div class="btn-event clearfix">
        <button class="btn-event-prev" type="button">이전 이벤트 보기</button>
        <button class="btn-event-next" type="button">다음 이벤트 보기</button>
      </div>
    </body>
  </html>
  ```


<br />

<br />

### 03 .related

#### 1. transition

- 변화를 관찰하고자하는 속성을 `transition` 속성으로 지정하면 hover 이벤트가 발생했을 때 부드러운 변화 효과를 기대할 수 있다.

  ```css
  .related-list {
    background: #fff;
    height: 25px;
    overflow: hidden;
    border: 1px solid #aaa;
    border-radius: 5px;
    transition: all 0.5s;
  }

  .related-list:hover {
    height: 145px;
    padding: 12px 0;
  }
  ```

<br />

#### 2. Tab 포커스 이벤트 대응

```javascript
$(document).ready(function() {
  
  // ...
  var list = $('.related-list');
  var last = $('.related-list li:last-child a');

  // 관련 사이트
  // list에 focusin 이벤트가 발생했을 때, 'list-open' 클래스를 동적으로 추가한다.
  list.focusin(function() {
    $(this).addClass('list-open');
  });

  // last에 focusout 이벤트가 발생했을 때, 'related-list' 클래스를 가진 부묘 요소를 찾아 해당 요소의 'list-open' 클래스를 동적으로 제거한다.
  last.focusout(function() {
    $(this).parents('.related-list').removeClass('list-open');
  });
});
```

<br />

<br />

### 04 .favorite

#### 1. em과 strong

- 단순히 꾸밈을 위한 용도라면 `span`으로 마크업하면 되겠지만, 의미를 갖는 영역이라면 시맨틱한 `em`, `strong`으로 마크업한다.

- sprite 이미지로 IR 기법으로 처리할 부분이 상승, 하락이라는 의미를 가진 영역이므로 `em`으로 마크업한다.

- `strong`은 좀 더 강한 강조, `em`은 비교적 약한 강조를 할 때 사용한다.

  ```html
  <!DOCTYPE html>
  <html>
    <head>
      <title>웹카페 - HTML5, CSS3, 웹접근성</title>
    </head>
    <body>
  	<div class="favorite">
        <h2 class="favorite-heading" id="favorite-heading">인기 <span>사이트</span></h2>
        <ol class="favorite-list">
          <li class="no1">W3C<em class="up">상승</em></li>
          <li class="no2">CSS Zen Garden<em class="down">하락</em></li>
          <li class="no3">Web Standards<em class="stop">멈춤</em></li>
          <li class="no4">Naver Cafe<em class="up">상승</em></li>
        </ol>
        <a href="#" class="favorite-more" aria-describedby="favorite-heading">더보기</a>
      </div>
    </body>
  </html>
  ```

<br />

#### 2. ol

- `ol`은 순서 있는 리스트를 마크업할 때 사용한다.
- 리스트의 순서를 `list-style: none`으로 지정하고 배경 이미지로 처리한다면 스크린 리더가 단순한 배경 이미지를 인식하지 못하므로 문제가 될 수 있다. `overflow: hidden`으로 화면에서 숨김 처리한 후 가상 요소를 적절히 사용한다면 이 문제를 해결할 수 있다.

##### 2.1 favorite-list li::before의 content를 한 번에 numbering 처리하는 방법 

- 각 list에 content를 직접 입력하지 않고 `counter-increment` 속성과 `counter` 함수를 이용하여 간단히  numbering할 수 있다.

  ```css
  .favorite-list li {
    counter-increment: number;
    margin-top: 5px;
    position: relative;
  }

  .favorite-list li::before {
    content: counter(number, decimal);
    color: #fff;
    background: #666;
    border-radius: 3px;
    padding: 0 5px;
    font-size: 1.2rem;
    margin-right: 5px;
  }
  ```

<br />

#### 3. inline 요소의 padding

-  inline 요소는 상하 padding을 가지지 못할 뿐, 좌우 padding은 가질 수 있다.

<br />

#### 4. vertical-align

- `vertical-align` 속성에 설정할 수 있는 다음과 같다. default는 `baseline`이다.
  - baseline
  - top
  - bottom
  - middle
- block 요소는 `vertical-align` 속성을 가질 수 없다.

<br />

#### 5. 수직 중앙 정렬

##### 5.1 transform 이용

- `position: absolute`와 `transform` 속성을 함께 사용하여 수직 중앙 정렬을 할 수 있다.

  ```css
  .favorite-list em {
    position: absolute;
    top: 50%;
    right: 0;
    transform: translateY(-50%);
  }
  ```

##### 5.2 음수 margin 이용

- 음수 margin을 사용해서 수직 중앙 정렬을 할 수 있다.

- 음수 margin을 사용할 때 % 단위가 아닌 px 단위로 설정해야 한다.

  ```css
  .favorite-list em {
    margin: -5px;
  }
  ```

<br />

#### 6. background의 position이 재정의되는 문제를 피하는 방법

- 속기법으로 `background` 속성을 정의하게 되면, 명시적으로 position을 설정하지 않았더라도 기본값인 0 0으로 position 속성이 설정된 상태가 된다. 따라서 이전에 선언하지 않은 줄 알았던 position을 설정하기 위해 다른 선택자를 사용했을 때,구체성 점수가 더 낮다면, 이미 한번 정의된 position의 값을 설정할 수 없는 문제가 발생한다. 이 문제는 background 개별 속성을 사용하면 간단히 해결된다.

  ```css
  .favorite-list em {
    background-image: url("images/rank.png");
    background-repeat: no-repeat;
    width: 9px;
    height: 11px;
    padding-top: 11px;
    overflow: hidden;
    position: absolute;
    top: 50%;
    right: 0;
    /* margin: -5px; */
    transform: translateY(-50%);

  }

  /* '.stop'과 '.down'의 구체성 점수가 '.favorite-list em'보다 더 낮지만, */
  /* '.favorite-list em'에서 개별 속성을 사용하였으므로 background-position 속성은 중복되지 않고 */
  /* '.stop'과 '.down'에서 설정한 값이 적용된다. */
  .stop {
    background-position: 0 50%;
  }

  .down {
    background-position: 0 100%;
  }
  ```

<br />

#### 7. 중복되는 코드의 처리 방법

##### 7.1 전처리기 활용

- Sass나 Less와 같은 전처리기를 이용하면 `@include`를 활용하여 중복된 코드의 사용을 줄일 수 있다.

##### 7.2 어트리뷰트 셀렉터 활용

- `[class$="more"]`: class 어트리뷰트가 "more"로 끝나는 요소를 선택한다.
- `[href^="https"]`: href 어트리뷰트가 :https"로 시작하는 요소를 선택한다.

<br />

#### 8. position

- `position: absolute`를 선언하면 해당 요소는 block 요소가 된다.
- 하지만 `position: relative`를 선언했을 땐 요소의 display가 block으로 바뀌지 않는다.

<br />

#### 9. 디자인 순서

- 되도록이면 바깥에서 안으로, 마크업 순서대로 디자인을 하는 습관을 들이는 것을 권장!

<br />

<br />

### 05 .slogan  

#### 1. heading 

- 웹 사이트의 성격을 고민해봤을 때, 이미지라 하더라도 그 뜻과 닿아있다면 heading으로 처리해도 적절하다. 적절한 텍스트를 넣은 후에 IR 기법으로 글자를 덮어씌워 처리하면 된다.
- heading의 IR 처리를 위해 가상 클래스 방법을 사용할 때, 가상 클래스인 `::before`, `::after`는 빈 내용이더라도 반드시 content 속성의 값이 존재해야 상자가 준비된다.
- `position: absolute`는 **자신의 조상 요소 중에 static이 아닌 가장 가까운 요소를 기준으로 자신의 위치를 설정**하므로, 부모 요소가 꼭 relative일 필요는 없다. absolute여도 가능하다.

<br />

#### 2. blockquote와 q

- `blockquote`와 `q`는 모두 인용구를 처리할 때 사용하는 태그이다.
- `cite` 어트리뷰트로 출처 정보를 밝힐 수 있다.
- 저작권에 대한 경각심을 가질 필요가 있다. 책에서 인용한 정보라면 *ISBN Number*를 남기면 된다.

##### 2.1 blockquote

- `blockquote`는 block 형태의 인용 관련 태그이다.
- agent style로 양쪽 여백 '들여쓰기'가 생긴다.

##### 2.2 q

- `q`는 inline 형태의 인용 관련 태그이다.

- agent style로 텍스트 양 끝에 격따옴표가 들어간다.

- `quotes` 속성을 이용하여 기본 스타일을 변경할 수 있다.

  ```css
  .slogan-content q {
    font-weight: bold;
    quotes: "<<" ">>";
  }
  ```

<br />

#### 3. 문서 내에 header나 footer는 반드시 1개?

- 본문의 footer 이외에 article 영역 또한 따로 footer를 가질 수도 있다.
- header나 footer 모두 section이나 article 또는 body 안에 각각 존재할 수도 있다.