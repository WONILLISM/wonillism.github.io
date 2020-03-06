---
title: "[WEB] 404 page 만들기 02"
excerpt: "404 page 만들기 CSS 구조"

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

last_modified_at: 2020-03-06
--- 
> __WEB__ 공부  
> 개발 언어 : __HTML, CSS, Javascript__  
> 개발 환경 : __Visual studio Code__   
> [참조: CODING FACTORY](https://www.codingfactory.net/)  

## __구조(Structure)__  

```
body
├───nav
│       ├nav-HOME
│       └nav-contactus
├───main
│       ├message-404
│       ├collage-404
│       └color-search
└───footer
        └search
```

## __CSS__  
```css 
@charset "utf-8";

/* init html, body*/
html,body{
    margin: 0; 
    padding: 0; 
    width: 100%; 
    height: 100%;
}
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
main p{
    max-width: 28em;
    margin: 1rem auto;
}
.input{
    position: relative;
    display: inline-flex;
}
nav{
    padding: 1rem;
}
footer{
    padding: 1rem;
}

input[type="search"] {
    background-color: #F1F3F4;
    font-size: 0.875rem;
    padding: 0.5em 1em;
    padding-right: 0.75em;
    border-radius: 1.25em;
    border: 0;
    width: 20em;
    transition: all 0.1s ease-in-out;
    box-shadow: 0 0 0 0 transparent;
    -webkit-appearance: none;
    appearance: none
}
input[type="search"]:hover {
    background-color: #e3e7e9
}
input[type="search"]:focus {
    outline: 0;
    box-shadow: 0 0 0 0.15em #ea4c89;
    background-color: #fff
}
input[type="search"]::-webkit-input-placeholder {
    color: rgba(0, 0, 0, 0.35)
}
.input{
    position: relative;
    display: flex;
    padding-left: 2rem;
}
.input-icon {
    position: absolute;
    left: 0.5rem;
    top: 50%;
    opacity: 0.3;
    pointer-events: none;
    transform: translateY(-50%)
}

body{
    font-size: 16px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    flex-direction: column;
    padding: 1rem;
    text-align: center;
    transition: background-color 1s linear;
}  
a{
    color: inherit;
    transition: all 0.1s ease-in;
}
a:hover{
    color: rgba(0, 0, 0, 0.8);
}
.color-range{
    position: relative;
    -webkit-appearance: none;
    appearance: none;
    width: 66%;
    max-width: 320px;
    display: block;
    outline: none;
    margin: 0 auto;
    height: 4em;
    font-size: 12px;
}
.color-range:focus{ 
    outline: none;
}
.color-range:active, 
.color-range:hover:active{
    cursor: grabbing; 
    cursor: -webkit-grabbing;
}
.color-range::-webkit-slider-runnable-track{
    -webkit-appearance: none;
    appearance: none;
    outline: none !important;
    background-color: rgba(0,0,0,0.1);
    border-radius: 0.5em;
    height: 0.5em;
    background: linear-gradient(to right, red,yellow,green,cyan,blue, #f0f, red);
}
.color-range:disabled{
    -webkit-filter: grayscale(100) opacity(0.25);
    filter:grayscale(100) opacity(0.25);
    pointer-events: none;
}
.color-range::-webkit-slider-thumb {
    height: 3em;
    width: 3em;
    margin-top: -1.2em;
    border-radius: 2em;
    -webkit-appearance: none;
    appearance: none;
    background: white;
    border: 0.4em solid currentColor;
    cursor: pointer;
    cursor: move;
    cursor: grab;
    cursor: -webkit-grab;
    transition: box-shadow 0.2s ease-in-out, m 0.1s ease-in-out;
    box-shadow: 0 0.1em 0.1em rgba(0, 0, 0, 0.05)
}
.color-range::-webkit-slider-thumb:active,
.color-range::-webkit-slider-thumb:hover:active {
    cursor: grabbing;
    cursor: -webkit-grabbing;
    transform: scale(0.975);
    box-shadow: 0 0 1px rgba(0, 0, 0, 0.1);
    border: 1.5em solid currentColor
}
.color-range::-webkit-slider-thumb:hover {
    transform: scale(1.1);
    box-shadow: 0 0.4em 1em rgba(0, 0, 0, 0.15)
}
.message-404{
    position: relative;
}
.collage-404{
    position: relative;

    perspective: 500px;
    display: inline-block;
    margin: 2vw 0;
}
.collage-404 h1{
    font-size: 30vw;
    margin: 0;
    line-height: 1;
    padding: 0;
    display: inline-block;
    transition: all 1s ease-in-out;
    opacity: 0.6;
}

nav{
    font-size: 1.3rem;
    font-weight: bold;
    display: flex;
    align-self: stretch;
    align-items: center;
    justify-content: space-between;
}
```

  

### init html, body  

```css  
/*  */
html,body{
    margin: 0; 	
    padding: 0; 
    width: 100%; 
    height: 100%;
}
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



+ __html, body__ : __html__의 기본 태그인 __html__과 __body__ 부분의 __margin과 padding__ 을 0으로 지정하고 현재 브라우저의 __너비(width)__와 __높이(height)__를 받아와 __100%__로 지정
+ __html__(현재 페이지)의   __box-sizing__ 방법을 __border-box__로 지정  

__box-sizing__의 요소

|    요소     |                     기능                     |
| :---------: | :------------------------------------------: |
| content-box |    __콘텐트 영역__을 기준으로 크기를 정함    |
| border-box  |   __테두리(border)__ 기준으로 크기를 정함    |
|   initial   | __기본값(content-box)__ 기준으로 크기를 정함 |
|   inherit   |      __부모 요소의 속성값__을 상속 받음      |

[![](/assets/Web/404page/2020-03-06-Web-404notfoundpage-02-img01.png)](/assets/Web/404page/2020-03-06-Web-404notfoundpage-02-img01.png)  

[출처: Coding factory 블로그](https://www.codingfactory.net/10630)  

+ __'*'(전체 선택자)__  : 모든 요소를 선택하는 선택자  

+ __`:before`,`:after`__ (가상 요소) :   box-sizing을 상속받음

  

__가상 클래스__ :  선택될 요소의 특별한 상태를 지정하는 선택자

__가상 요소__ :  가상 클래스 처럼, 가상 요소는 선택자에 추가되지만 특별한 상태를 기술하는 대신 문서의 특정 부분을 스타일 할 수 있다.   

#### link

|                  가상 클래스(pseudo-class)                   |                  가상 요소(pseudo-element)                   |
| :----------------------------------------------------------: | :----------------------------------------------------------: |
| [`:active`](https://developer.mozilla.org/ko/docs/Web/CSS/:active) | [`::after`](https://developer.mozilla.org/ko/docs/Web/CSS/::after) |
| [`:any`](https://developer.mozilla.org/ko/docs/Web/CSS/:any) | [`::before`](https://developer.mozilla.org/ko/docs/Web/CSS/::before) |
| [`:checked`](https://developer.mozilla.org/ko/docs/Web/CSS/:checked) | [`::first-letter`](https://developer.mozilla.org/ko/docs/Web/CSS/::first-letter) |
| [`:default`](https://developer.mozilla.org/ko/docs/Web/CSS/:default) | [`::first-line`](https://developer.mozilla.org/ko/docs/Web/CSS/::first-line) |
| [`:dir()`](https://developer.mozilla.org/ko/docs/Web/CSS/:dir) | [`::selection`](https://developer.mozilla.org/ko/docs/Web/CSS/::selection) |
| [`:disabled`](https://developer.mozilla.org/ko/docs/Web/CSS/:disabled) | [`::backdrop`](https://developer.mozilla.org/ko/docs/Web/CSS/::backdrop) |
| [`:empty`](https://developer.mozilla.org/ko/docs/Web/CSS/:empty) | [`::placeholder`](https://developer.mozilla.org/ko/docs/Web/CSS/::placeholder) |
| [`:enabled`](https://developer.mozilla.org/ko/docs/Web/CSS/:enabled) | [`::marker`](https://developer.mozilla.org/ko/docs/Web/CSS/::marker) |
| [`:first`](https://developer.mozilla.org/ko/docs/Web/CSS/:first) | [`::spelling-error`](https://developer.mozilla.org/ko/docs/Web/CSS/::spelling-error) |
| [`:first-child`](https://developer.mozilla.org/ko/docs/Web/CSS/:first-child) | [`::grammar-error`](https://developer.mozilla.org/ko/docs/Web/CSS/::grammar-error) |
| [`:first-of-type`](https://developer.mozilla.org/ko/docs/Web/CSS/:first-of-type) |                                                              |
| [`:fullscreen`](https://developer.mozilla.org/ko/docs/Web/CSS/:fullscreen) |                                                              |
| [`:focus`](https://developer.mozilla.org/ko/docs/Web/CSS/:focus) |                                                              |
| [`:hover`](https://developer.mozilla.org/ko/docs/Web/CSS/:hover) |                                                              |
| [`:indeterminate`](https://developer.mozilla.org/ko/docs/Web/CSS/:indeterminate) |                                                              |
| [`:in-range`](https://developer.mozilla.org/ko/docs/Web/CSS/:in-range) |                                                              |
| [`:invalid`](https://developer.mozilla.org/ko/docs/Web/CSS/:invalid) |                                                              |
| [`:lang()`](https://developer.mozilla.org/ko/docs/Web/CSS/:lang) |                                                              |
| [`:last-child`](https://developer.mozilla.org/ko/docs/Web/CSS/:last-child) |                                                              |
| [`:last-of-type`](https://developer.mozilla.org/ko/docs/Web/CSS/:last-of-type) |                                                              |
| [`:left`](https://developer.mozilla.org/ko/docs/Web/CSS/:left) |                                                              |
| [`:link`](https://developer.mozilla.org/ko/docs/Web/CSS/:link) |                                                              |
| [`:not()`](https://developer.mozilla.org/ko/docs/Web/CSS/:not) |                                                              |
| [`:nth-child()`](https://developer.mozilla.org/ko/docs/Web/CSS/:nth-child) |                                                              |
| [`:nth-last-child()`](https://developer.mozilla.org/ko/docs/Web/CSS/:nth-last-child) |                                                              |
| [`:nth-last-of-type()`](https://developer.mozilla.org/ko/docs/Web/CSS/:nth-last-of-type) |                                                              |
| [`:nth-of-type()`](https://developer.mozilla.org/ko/docs/Web/CSS/:nth-of-type) |                                                              |
| [`:only-child`](https://developer.mozilla.org/ko/docs/Web/CSS/:only-child) |                                                              |
| [`:only-of-type`](https://developer.mozilla.org/ko/docs/Web/CSS/:only-of-type) |                                                              |
| [`:optional`](https://developer.mozilla.org/ko/docs/Web/CSS/:optional) |                                                              |
| [`:out-of-range`](https://developer.mozilla.org/ko/docs/Web/CSS/:out-of-range) |                                                              |
| [`:read-only`](https://developer.mozilla.org/ko/docs/Web/CSS/:read-only) |                                                              |
| [`:read-write`](https://developer.mozilla.org/ko/docs/Web/CSS/:read-write) |                                                              |
| [`:required`](https://developer.mozilla.org/ko/docs/Web/CSS/:required) |                                                              |
| [`:right`](https://developer.mozilla.org/ko/docs/Web/CSS/:right) |                                                              |
| [`:root`](https://developer.mozilla.org/ko/docs/Web/CSS/:root) |                                                              |
| [`:scope`](https://developer.mozilla.org/ko/docs/Web/CSS/:scope) |                                                              |
| [`:target`](https://developer.mozilla.org/ko/docs/Web/CSS/:target) |                                                              |
| [`:valid`](https://developer.mozilla.org/ko/docs/Web/CSS/:valid) |                                                              |
| [`:visited`](https://developer.mozilla.org/ko/docs/Web/CSS/:visited) |                                                              |

가상 선택자는 __꾸밈을 위해서 의미없는 태그를 더 추가__ 해야 될 때, 태그 대신에 가상으로 처리해 주는 기능.    

  

__font-size 단위__   

```css
font-size: medium | xx-small | x-small | small | large | x-large | xx-large | smaller | larger | length | initial | inherit
```

- medium : 웹브라우저에서 정한 기본 글자크기
- xx-small, x-small, small, large, x-large, xx-large : medium에 대한 상대적인 크기
- smaller, larger : 부모 요소의 글자 크기에 대한 상대적인 글자 크기
- length : px, %, em, rem 등으로 크기를 정함
- initial : 기본값으로 설정
- inherit : 부모 요소의 속성값을 상속받음  

```css
font-size: length
```

- 웹브라우저의 기본 글자 크기는 보통 16px
- %와 em은 부모 요소의 글자 크기에 대한 상대적인 글자 크기입니다. 100%와 1em은 부모 요소의 글자 크기와 같고, 숫자가 커질수록 글자가 커지고, 숫자가 작아질수록 글자가 작아진다.
- rem은 최상위 요소, 즉 html 요소의 글자 크기에 대한 상대적인 글자 크기  



#### Box Model  

+ __박스의 구성__
  + __margine area__(바깥 영역)  
  + __border area__(테두리 영역)  
  + __padding area__(안쪽 여백 영역)
  + __content area__(내용 영역)  
+ __각 영역을 꾸밀 때 사용하는 속성__  
  + 바깥 여백 : margin 속성
  + 테두리 : border 속성
  + 안쪽 여백 : padding 속성
  + 박스의 가로 크기 : width 속성
  + 박스의 세로 크기 : height 속성
  + 박스의 크기 기준 : box-sizing 속성
  + 박스의 배경 : background 속성

[![](/assets/Web/404page/2020-03-06-Web-404notfoundpage-02-img02.png)](/assets/Web/404page/2020-03-06-Web-404notfoundpage-02-img02.png)   

  

#### line-height  

줄 높이를 지정하는 속성

```css  
line-height: normal | length | number | percentage | initial | inherit
```

- normal : 웹브라우저에서 정한 기본값입니다. 보통 1.2
- length : 길이로 줄 높이를 정함
- number : 글자 크기의 몇 배인지로 줄 높이를 정함
- percentage : 글자 크기의 몇 %로 줄 높이로 정함
- initial : 기본값으로 설정합니다.
- inherit : 부모 요소의 속성값을 상속받습니다.  



