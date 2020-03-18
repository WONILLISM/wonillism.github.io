---
title: "[WEB] 404 page 만들기 03"
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

last_modified_at: 2020-03-09
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

### body layout  

```css  
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
```

이 page의 몸통이 되는 body 부분이다.  

+ **font-size: 16px** - **body** 의 모든 기본 폰트 사이즈 **16px** 로 고정

+ **display: flex** - 화면에 보여지는 속성을 **flex** 로 지정  

  + [CSS flex(flexible box) 완벽 가이드](https://heropy.blog/2018/11/24/css-flexible-box/)  

+ **justify-content** : 주 축(main-axis)의 정렬방법 설정

+ **align-items** : 교차 축(cross-axis)에서 Items의 정렬 방법을 설정(1줄)

  (여러 줄인 경우 align-content 를 사용)

  + **align-content, align-items** 속성
    + **stretch** : Container의 교차 축을 채우기 위해 items를 늘림 (기본값)
  + **justify-content, align-content, align-items** 모두 사용
    + **flex-start** : Items를 시작점으로 정렬  
    + **flex-end** : Items를 끝점으로 정렬  
    + **center** : Items를 가운데 정렬  
    + **space-between** : 시작 Item은 시작점에, 마지막 Item은 끝점에 정렬되고 나머지 Items는 사이에 고르게 정렬됨  
    + **space-around** : Items를 균등한 여백을 포함하여 정렬

+ **flex-direction** : flex items의 주 축(main-axis)을 설정

  + **row** : 수평축, 왼쪽에서 오른쪽 ( 기본 값 )
  + **row-reverse** : 수평축, **row** 의 반대
  + **column** : 수직축, 위에서 아래
  + **column-reverse** : 수직축, **column** 의 반대

+ **text-align** : 문단 정렬 방식 설정

+ **transition** : css속성을 변경할 때 애니메이션 속도를 조절하는 방법  



### color range  

```css
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

  

+ **position** :  태그들의 위치를 결정하는 속성  
  + **static(기본값)** : 모든 태그들은 왼쪽에서 오른쪽 위에서 아래로 쌓인다.
  + **relative** : 태그들의 위치를 살짝 변경하고 싶을 때 사용, **top** , **bottom** , **right** ,**left** 를 이용해 위치 조절 가능  
  + **absolute** : **relative** 가 **static** 을 기준으로 주어진 픽셀만큼 움직였다면, **absolute** 는 **position: static** 속성을 가지고 있지 않은 **부모를 기준** 으로 움직임, 부모 중 **position** 이 **relative** , **absolute** , **fixed** , 인 태그가 없다면 최상위 태그 **body** 를 기준으로 움직임  
  + **fixed** : 항상 특정 위치에 고정  
+ **appearance** : 운영체제 및 기본 브라우저에 설정되어 있는 테마를 기반으로 요소를 표현한다.  
  + **webkit-appearance** : safari 나 chrome 에서 사용
  + **-moz-appearance** : fierfox에서 사용
  + **none** : 네이티브로 지원되는 모양들을 해제
+ **border-radius** : 태두리 박스의 모서리를 둥글게 지정할 때 사용    