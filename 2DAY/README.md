# FDS 7기 강의 내용 정리(2017년 11월 14일) 

## Session

### 01 HTML5

#### 1.1 기존 HTML의 약점(~ HTML 4.01)

1. 대소문자를 구분하지 않는다.

2. 속성의 값을 ""로 묶지 않아도 된다.

3. 클로징 태그를 생략해도 문제가 발생하지 않는다.

   → ***자유도가 너무 높다!***

<br>

#### 1.2 새로운 HTML의 등장 

1. 이러한 기존 HTML의 약점을 보완하기 위해 W3C는 XML 기반의 새로운 HTML인 XHTML 1.0을 재정의하기 시작

2. XHTML의 특징

   1) 모든 태그는 소문자로 작성

   2) 모든 속성의 값은 반드시 격따옴표로 묶여야 한다.

   3) 모든 속성은 반드시 값을 가져야 한다. 

   4) 모든 태그 요소는 셀프 클로징을 가져야 한다.

3. XHTML은 하위 호환성 등에 많은 문제가 있었고 W3C는 공식적으로 XHTML의 실패를 인정

<br>

#### 1.3 새로운 표준, HTML5

1. WHATWG가 W3C와는 별개로 XHTML과는 다른 별도의 표준 스펙을 만들어내기 시작

2. W3C가 WHATWG의 표준안을 대부분 수용하게 되면서 새로운 표준의 HTML5가 탄생

3. HTML5 기술 안에는 **Markup**과 **API 기술**이 함께 포함되어 있다.

4. 아웃라인 알고리즘

   - 기존의 HTML 4.01에서는 heading의 레벨에 따라 암묵적으로 연결된 컨텐츠를 구분
   - HTML5에서는 아웃라인 태그로 연결된 컨텐츠를 구분
   - heading의 레벨이 중요한 것이 아니라 자신의 부모가 누구인지가 중요

   ```html
   <!-- HTML 4.01 방식 -->
   <!-- heading의 레벨에 따라 연결된 컨텐츠를 구분한다. -->
   <!-- 'h1 + p' 와 'h2 + p'는 구분된 섹션 -->
   <h1>
     Heading 1
   </h1>
   <p>
     Section 1
   </p>
   <h2>
     Heading 2
   </h2>
   <p>
     Section 2
   </p>

   <!-- HTML5 방식 -->
   <!-- 아웃라인 태그로 연결된 컨텐츠를 구분한다. -->
   <!-- header 섹션과 main 섹션은 구분된 섹션 -->
   <header>
   	<h1>Heading 1</h1>
     	<h2>hader section</h2>
   </header>
   <main>
   	<p>main section</p>
   </main>
   ```

<br>

#### 1.4 HTML5 Markup 기초

1. 특수문자 입력
   - &lt: less than, <
   - %gt: greater than, >
2. [Reference](https://github.com/seulbinim/FC-FDS/blob/master/PDF/HTML5.pdf "Markup 기초")

> **DTD(Document Type Definition)**
>
> 1. Strict DTD: 시각적(CSS) 요소의 사용을 허용하지 않는다.
> 2. Transitional DTD: 과도기 모드
> 3. Frame DTD

<br>

<br>

### 02 CSS3 레이아웃

#### 2.1 width는 가능한 고정하지 않는 것을 권장 

1. width는 auto(Default Value)로 설정하여 컨텐츠의 길이에 따라 자연스럽게 늘어나게 하는 것을 권장

<br>

#### 2.2 배치 조정

1. float: 구형 브라우저까지 고려할 때 사용
2. flexbox: 모던 브라우저에 맞출 때 사용
3. grid: 모던 브라우저에 맞출 때 사용

<br>

#### 2.3 색상 조정 방법

1. rgb 16진수 방식
   - 앞에서부터 두 자리씩 Red, Green, Blue를 나타내는 색상 값
   - 색상별로 같은 값이 반복될 때 short-hand 방식으로 세 자리로 축약하여 나타낼 수 있다. (#AA55BB →#A5B) 
2. rgb 10진수 방식
   - rgba(255, 0, 0, 0, 5)

<br>

#### 2.4 vh(Viewport Height)

1. 높이를 나타내는 단위로 px, %, em 이외에 vh를 사용할 수 있다.
2. 1vh는 디바이스 화면 높이의  1 / 100의 크기를 의미한다.
3. vh와 % 모두 상대 크기를 나타내는 단위로 헷갈릴 수 있다.
   - vh: 디바이스 화면 높이를 기준으로 상대적 크기를 정함.
   - %: 해당 요소가 속한 부모 요소의 content 영역의 높이를 기준으로 상대적 크기를 정함. 

<br>

#### 2.5 그룹 선택자

1. 그룹 선택자(,)를 이용해 공통된 성질을 한 번에 선언할 수 있다.

```css
div, p, h1 {
  background-color: yellow;
}
```

2. 모든 스타일에 대해 공통으로 적용할 수 있으므로 유지보수하기 편리하다.

<br>

#### 2.6 가운데 정렬

1. CSS2에서는 가운데 정렬이 없지만(margin: 0 auto; 는 트릭에 불과하다) CSS3에서는 flexbox를 이용하면 가운데 정렬이 가능하다.

> User Agent Style
>
> 브라우저가 갖고 있는 default style을 의미한다.

<br>

#### 2.7 flexbox

1. `display: flex;`: 해당 요소 안의 모든 엘리먼트가 **flex item으로 변경**된다.
2. `flex-direction`의 default는 **row**이다.
3. 모바일 웹 개발 시 box-sizing은 **content-box보다 border-box가 더 유리**하다.
4. `margin: 0 auto;`는 브라우저 뷰포트에서 width를 제외한 나머지를 자동으로 절반으로 나누어 처리한다. 즉, 실제로 가운데 정렬이 일어난 것이 아니라 **margin 영역은 눈에 보이지 않는 영역이기 때문에 가운데 정렬처럼 보이는 것**이다.
5. justify-content: flex-direction에 설정된 방향에 대한 정렬 설정**(메인 축)**
6. align-items: 교차점 정렬 설정**(교차점)**
7. justify-content의 default는 **flex-start**이다.
8. `justify-content`

```css
.between {
  justify-content: space-between; /* 남는 역역을 잘라서 between 값을 자동 계산 */
}

.around {
  justify-content: space-around; /* 양쪽에 여백까지 할당 */
}
```

9. align-items는 해당 요소 내의 모든 아이템을 정렬할 때, align-self는 자신만 정렬할 때 사용한다.
10. 요소 간에 정렬 순서를 변경할 때에는 마크업 순서로 배치를 바꾸는 것이 아니라 **flexbox의 order 프로퍼티를 사용하여 정렬 순서를 변경**한다. order 프로퍼티의 **default는 0**이다.
11. flexbox는 자신의 container보다 width가 클 때, **각 아이템의 width를 아아서 비율에 맞게 계산**한다.
12. flexbox의 width가 container보다 width를 넘었을 떄 줄을 변경하고 싶다면 **`flex-wrap: wrap;`을 설정**하면 된다.
13. flex-wrap의 **default는 no-wrap**이다.
14. flex-flow로 **flex-direction과 flex-wrap을 한 번에 설정**할 수 있다.
15. align-items는 단일 행, 열일 때 사용하고 align-content는 다중 행, 열일 때 사용한다.

<br>

#### 2.8 float

1. float의 **default는 none**이다.
2. float는 left, right 정렬만 가능할 뿐, 속성 값에 center를 주는 것은 불가능하다.
3. clear 프로퍼티는 **Block Element**에만 사용 가능하다.
4. 가상 요소 선택자(:after, ::after)
   - :을 하나만 찍으면 예전 방식, 2개 찍는 것이 요즘 방식



<br>

<br>

## VScode

### 01 Shortcut

1. 명령 팔레트 실행: Cmd(Ctrl)) + Shift + 'P'
2. 약어로 래핑: 래핑할 블록 선택 → [명령 팔레트] 실행 → emmet 검색 → [약어로 래핑] → 'div.footer-bg' 입력 후 엔터
3. 주석 처리: Cmd(Ctrl) + '/'

<br>

### 02 Extension

1. Path Autocomplete: path 자동 완성 기능

<br>

### 03 Preference

1. 들여쓰기 수정하기: [명령 팔레트] → [formatter config] → indent.size = 2로 수정 → vscode 재실행
2. minimap, fontsize 수정하기: 위와 비슷한 방법으로 설정할 수 있다.


<br>

<br>


## ETC

### 01 Bookmark

1. [https://www.w3.org/](https://www.w3.org/) 'Markup Validation Service'를 이용하여 HTML 문법을 검사할 수 있다.
2. [html5test.com](html5test.com) 사용 중인 브라우저가 HTML5 스펙을 얼마나 지원하는지 확인할 수 있다.
3. [css3test.com](http://css3test.com/) 사용 중인 브라우저가 CSS3 모듈을 얼마나 지원하는지 확인할 수 있다.
4. [csszengarden.com](http://csszengarden.com/) 하나의 html 문서에 대해 다양한 CSS 레이아웃을 적용해볼 수 있다.
5. [naradesign.net/wp/](naradesign.net/wp/) 웹 관련 기술 블로그

