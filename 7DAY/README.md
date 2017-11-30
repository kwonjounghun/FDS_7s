## 2017.11.21 6조 정리

### word-wrap 
word-wrap: normal, break-word 두 가지의 속성
1. normal : 글자를 줄바꿈하지 않고 한 줄에 표시
2. break-word : 글자를 줄바꿈해서 표현

### ARIA 속성
ARIA란? Accessible Rich Internet Applications의 약자로 web contens를 장애가 있는 사람들에게 쉽게 접근할 수 있도록 만든 웹접근방식

```
<div class="pds">
    <h2 id="pds-heading" class="pds-heading" tabindex="0">자료실</h2>
    <a href=# class="pds-more board-act" aria-labelledby="pds-heading">더보기</a>
</div>
```
위의 a tag에서 title을 쓸 수도 있으나 aria-labelledby의 중복이므로 쓰지 않는다.

aria-labelledby - 보충하는 단어를 설명할 때 사용
aria-describedby -  보충하는 문장을 설명할 때 사용

[참고자료][https://slack-redir.net/link?url=https%3A%2F%2Fdevelopers.google.com%2Fweb%2Ffundamentals%2Faccessibility%2Fsemantics-aria%2Faria-labels-and-relationships%3Fhl%3Dko]

### text-overflow
영역을 넘어간 텍스트를 생략부호로 표시하는 방법.
기본값 : clip
ellipsis 잘린 텍스트를 생략부호로 표시

### white-space
nowrap은 텍스트가 길어도 줄바꿈을 하지 않음
normal은 줄바꿈이 됨(기본값)