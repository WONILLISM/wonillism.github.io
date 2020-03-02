---
title: "[WEB] 404 page 만들기 01"
excerpt: "404 page 만들기"

categories:
    - WEB
tags:
    - javascript
    - 자바스크립트
    - vanilla JS
    - vanilla
    - html
    - css
    - 404 page
    - 웹 개발
    - 프론트 엔드
    - front end
use_math: true;
last_modified_at: 2020-03-02
--- 
> __WEB__ 공부  
> 개발 언어 : __HTML, CSS, Javascript__  
> 개발 환경 : __Visual studio Code__  

## __구조(Structure)__  
  
```
body
├───nav
├───main
│       ├section01
│       ├section02
│       └section03
└───footer
        └search
```
    
## __HTML__  
`index.html (body 이하)`  
```html  
<nav>
    <a class="logo" href="https://llism.github.io">logo</a>
    <span>
        <button>Contact us</button>
    </span>
</nav>  
  
<main>
    <section class="01">
    </section>
    <section class="02">
    </section>
    <section class="03">
    </section>
</main>
<footer>
    <form id="search" action="">
        
    </form>
</footer>
```  
  
> __`article`, `section`, `div` 차이__   
> __article__ : 독립적이고 홀로 설 수 있는 내용 (블로그 글, 포럼 글, 뉴스 기사 등)  
> __section__ : 내용이 서로 연관되어 있는 문서를 구분할 때  
> __div__ : 의미적으로 관계가 없을 때(오직 내용을 묶는 역할)  
> 
> `form` tag  
> 웹 페이지에서의 입력 양식을 의미(로그인 창, 회원가입 폼, 검색 창 등)  
> 텍스트 필드에 글자를 입력하거나, 체크박스나 라디오버튼을 클릭하고 제출 버튼을 누르면 __백엔드 서버__ 에 양식이 전달되어 정보를 처리하게 됨.  
  
## __CSS__  
  
### __init__  
```css  
/* init html, body*/
html, body{
    margin: 0; 
    padding: 0; 
    width: 100%; 
    height: 100%;}

html{
    box-sizing:  border-box;
}
*,
*:before,
*:after {
    box-sizing: inherit
}
h1{
    font-size: 2rem; 
    margin: 1rem 0; 
    line-height: 1;
}
p{
    margin: 1rem 0; 
    line-height: 1.3;
}
```
> __%와 vw/vh 차이__  
> __%__ : 스크롤 바를 포함하지 않음  
> __vw/vh__ : viewport width, viewport height의 의미  
> 스크롤 바를 포함  
>   
> __box-sizing__ : 박스의 크기를 어떤 것으로 계산할 지 정하는 속성  
> (content-box | border-box | initial | inherit)  
> content-box : 콘텐츠 영역 기준  
> border-box : 테두리 기준  
> initial : 기본값 기준(content-box, 상속 no, 애니메이션 no)  
> inherit : 부모 상속   
> 
> __rem__ : 문서의 최상위 요소, 즉 html의 요소 크기에 비례  
> 
   
## __nav__  
  
```css  
/* nav */
nav{
    padding: 1rem;

    display: flex;
    align-self: stretch;
    align-items: center;
    justify-content: space-between;
}
```  

## __main__  
작성중...

  
