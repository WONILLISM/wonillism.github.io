---
title: "[Making_Blog] 웹 표준 사이트 만들기 02"
excerpt: "실전! 기본 레이아웃, 스킵메뉴, 메뉴 만들기"

categories:
    - Make_Blog
tags:
    - Blog  
    - 블로그 만들기
    - jekyll
    - github blog
    - 깃헙 블로그
    - jekyll theme
    - 지킬 테마
    - minimal-mistakes  
    - Web
    - 웹
    - html
    - css
last_modified_at: 2019-12-26
---   
__참조__ : <https://webzz.tistory.com/>  
앞에서 배웠던 레이아웃 만드는 방법들을 이용하여 기본 레이아웃을 만들어 보자.  
  
### Layout  

[![img01](..\assets\Make_Blog\2019-12-26-Makeblog-Website-02-img01.JPG)](..\assets\Make_Blog\2019-12-26-Makeblog-Website-02-img01.JPG)  

[CODE](https://github.com/WONILLISM/Study_web/commit/c77f9e88cdddf59f2bf69d3e755dd9554be8b319)  

위와 같은식으로 `헤더`, `콘텐츠 네비게이션`, `콘텐츠 타이틀`, `콘텐츠 배너`, `세부 콘텐츠`, `풋터` 로 구분하여 만들 예정이다.  
  
### Skip Menu  
  
마우스를 사용할 수 없는 상활일 때 사용하는 스킵메뉴를 추가했다.  
평소에는 보이지 않다가 `Tap`을 눌렀을 때 보여지는 메뉴다.  

[![img02](..\assets\Make_Blog\2019-12-26-Makeblog-Website-02-img02.JPG)](..\assets\Make_Blog\2019-12-26-Makeblog-Website-02-img02.JPG)  
  
[CODE](https://github.com/WONILLISM/Study_web/commit/0d84e564b5a61656d760fcba59665c8f7c587297)  
  
### 헤더 배경 및 메뉴 만들기  
  
※Tip

+ text는 `padding`값이 좌 우 밖에 먹히지 않는다  
```css 
    header .header-menu a {color: #fff; padding: 10px 10px 10px 13px; display: inline-block;}  
```  

+ 위와 같이 `display:inline-block`으로 해결한다.
  
[![img03](..\assets\Make_Blog\2019-12-26-Makeblog-Website-02-img03.JPG)](..\assets\Make_Blog\2019-12-26-Makeblog-Website-02-img03.JPG)  

[CODE](https://github.com/WONILLISM/Study_web/commit/f140c81642db8ab3801fa3365347bc91b18c09bf)  