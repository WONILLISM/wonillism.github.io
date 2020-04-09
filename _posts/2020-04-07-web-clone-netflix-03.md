---
title: "[WEB] Netflix 따라 만들기 03. CSS 구조"
excerpt: "Netflix 따라 만들기"

categories:
    - WEB
tags:
    - 넷플릭스
    - Netflix
    - coding test
    - front end
    - 프론트 엔드
    - vanilla javascript
    - 자바스크립트
    - tmdb
    - the movie database
    - html
    - css
    - clone
use_math: true;

last_modified_at: 2020-04-07  
---

{% include GoogleAdSenseSidebar.html %}  

## CSS 구조 

```markdown
init.css
header.css
popularMovie.css
main.css
```

  



## init.css

```css
/* init */
html,	
body{
    margin: 0;
    padding: 0;
    width: 100%;
    height: 100%;
    background-color: rgb(10,10,10);
    font-size: 16px;
}
html{
    box-sizing: border-box;
    font-family: sans-serif;
}
*,
*:after,
*:before{
    box-sizing: inherit;
}
li, ul{
    margin: 0; padding: 0; border: 0; font-size: 100%; font: inherit; vertical-align: baseline;
}
ul{
    list-style: none;
}

```

  초기값들을 설정

## header.css

```css
/* layout */
header{
    top: 0; 
    background: transparent;
}
.header_container{
    display: flex;
    align-items: center;
}
.logo, .main_nav, .sub_nav{
    flex: 0 0 auto; /* flex: none */
}
.main_nav{
    display: flex;
    align-items: center;
    
}
.sub_nav{
    display: flex;
    align-items: center;
    margin-left: auto;
}

.header_container{
    width: 100%;
    /* fixed nav-bar */
    position: fixed;
    top: 0;
    left: 0;
    z-index: 2;

    background: linear-gradient(to bottom, rgba(0, 0, 0, 0.7) 10%, rgba(0, 0, 0, 0));
    color: #ddddff;
    font-size: 0.9rem;
}
.logo{
    padding-left: 1rem;
    text-decoration: none;
    text-align: center;
    line-height: 3rem;
    font-size: 3rem;
}
.logo a img{
    height: 1em;
}
.logo .header_toggleBtn{
    display: none;
}
.main_nav .main_nav_tab{
    padding-left: 1rem;
}
.sub_nav .sub_nav_tab{
    padding-right: 1rem;
}
```

### **header** 의 **navigation**  부분의 설정

```css
.header_container{
    display: flex;
    align-items: center;
}
.logo, .main_nav, .sub_nav{
    flex: 0 0 auto; /* flex: none */
}
.sub_nav{
    display: flex;
    align-items: center;
    margin-left: auto;
}
```

[![](/assets/web/clone_netflix/css_header_img01.png)](/assets/web/clone_netflix/css_header_img01.png)

오른쪽 정렬하고 싶은 항목들을 `margin-left: auto;` 처리해주면 된다.

### header 상단 고정

```cpp
.header_container{
    width: 100%;
    /* fixed nav-bar */
    position: fixed;
    top: 0;
    left: 0;
    z-index: 2;

    background: linear-gradient(to bottom, rgba(0, 0, 0, 0.7) 10%, rgba(0, 0, 0, 0));
    color: #ddddff;
    font-size: 0.9rem;
}
```



**header** 를 상단에 고정시키기 위해 `position: fixed; top: 0; left:0; z-index: 2;` 처리 



{% include GoogleAdSensePost.html %}  

