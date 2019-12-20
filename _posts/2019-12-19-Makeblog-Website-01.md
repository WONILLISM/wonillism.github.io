---
title: "[Making_Blog] 웹 표준 사이트 만들기 01"
excerpt: "웹 표준사이트 만들기-layout"

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
last_modified_at: 2019-12-19
---  
__jekyll theme__ 를 사용하지 않은 나만의 블로그를 만들기 위한 첫번째 단계!  
웹 페이지를 만들기위해서 구글링을 하다가 매우 괜찮은 사이트를 알아냈다. __HTML, CSS, JAVASCRIPT, JQuery 등__ 에 대해서 영상으로 강좌도 올려놓으시고 기초 부터 정리를 엄청 잘 해놓으셨다... 갓... 감사합니다.  
<https://webzz.tistory.com/>  
# 웹 표준 사이트 만들기 
우선 웹페이지의 틀을 만들기위해 `layout` 기본 설정을 해보자.  
__※__ tip  
+ `div*n` + `ctrl + space` or `tap` : n개의 `div`를 만들 때  
+ `w1000` , `h1000` : `width:1000px;` , `height:1000px;`
+ style에 적용할 때 id를 직접 치기보다는 복사해서 사용하자(오타에 대한 실수를 줄임)
+ `fll` + `ctrl + space` or `tap` : `float: left`

## layout 01
```html
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Layout01</title>

    <style>
        body{background:  #c8e6c9;}
        #wrap {width: 1000px;height: 900px;margin: 0 auto; font-size: 40px; color: #fff; text-align: center;text-transform: uppercase;}
        #header { width: 1000px; height: 100px; background: #2e7d32;}
        #nav { width: 1000px; height: 100px;background: #388e3c;}
        #side { float: left; width: 300px; height: 600px;background: #43a047;}
        #contents {float: left; width: 700px;height: 600px; background: #4caf50;}
        #footer { float: left; width: 1000px; height: 100px;background: #66bb6a;}
    </style>
</head>
<body>
    <div id="wrap">
        <div id="header">header</div>
        <div id="nav">nav</div>
        <div id="side">side</div>
        <div id="contents">contents</div>
        <div id="footer">footer</div>
    </div>
</body>
</html>
```  
  
[layout 01 ![](/assets\Make_Blog\2019-12-19-Makeblog-Website-01-img01.JPG)](/assets\Make_Blog\2019-12-19-Makeblog-Website-01-img01.JPG)
  
## layout 02
__※__ tip  
+ `claer: both` : `float: left` 성질을 차단시켜줌  
  

```html  
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Layout02</title>

    <style>
        body {background-color: #b3e5fc;}
        #wrap {width: 1000px; height: 900px; margin: 0 auto; font-size: 40px; color:#fff; text-align: center;}
        #header {width: 1000px; height: 100px; line-height: 100px; background-color: #0277bd;}
        #nav {width: 1000px; height: 100px; line-height: 100px; background-color: #0288d1;}
        #side_left {float: left; width: 300px; line-height: 600px;  height: 600px; background-color: #039be5;}
        #contents {float: left; width: 400px; line-height: 600px;  height: 600px; background-color: #03a9f4;}
        #side_right {float: left; width: 300px; line-height: 600px;  height: 600px; background-color: #29b6f6;}
        #footer {clear: both; width: 1000px; height: 100px; line-height: 100px; background-color: #0288d1;}
    </style>
</head>
<body>
    <div id="wrap">
        <div id="header">header</div>
        <div id="nav">nav</div>
        <div id="side_left">side_left</div>
        <div id="contents">contents</div>
        <div id="side_right">side_right</div>
        <div id="footer">footer</div>
    </div>
</body>
</html>
```  
  

[layout 02 ![](/assets\Make_Blog\2019-12-19-Makeblog-Website-01-img02.JPG)](/assets\Make_Blog\2019-12-19-Makeblog-Website-01-img02.JPG)  

  
## layout 03  
  

```html   
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Layout03</title>
    <style>
        body {background-color: #d1c4e9;}
        #wrap {width: 1000px; height: 900px; margin: 0 auto; font-size: 40px; color:#fff; text-align: center; }
        .side {float: left; width: 300px; height: 900px; line-height: 900px; background-color: #4527a0;}
        .header {float: left; width: 700px; height: 300px; line-height: 300px; background-color: #512da8;}
        .contents {float: left; width: 700px; height: 300px; line-height: 300px; background-color: #5e35b1;}
        .footer {float: left; width: 700px; height: 300px; line-height: 300px; background-color: #673ab7;}
    </style>
</head>
<body>
    <div id="wrap">
        <div class="side">side</div>
        <div class="header">header</div>
        <div class="contents">contents</div>
        <div class="footer">footer</div>
    </div>
</body>
</html>
```    
[layout 03 ![](/assets\Make_Blog\2019-12-19-Makeblog-Website-01-img03.JPG)](/assets\Make_Blog\2019-12-19-Makeblog-Website-01-img03.JPG)  
  

## layout 04  

```html  
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Layout04</title>
    <style>
    body {background-color: #ffe0b2;}
        #wrap {width: 1000px; height: 900px; margin: 0 auto; font-size: 30px; color:#fff; text-align: center; text-transform: uppercase;}
        .header {width: 1000px; height: 100px; line-height: 100px; background: #ef6c00;}
        .nav {width: 1000px; height: 100px; line-height: 100px; background: #f57c00;}
        .side {float: left; width: 300px; height: 600px; line-height: 600px; background: #fb8c00;}
        .contents1 {float: left; width: 700px; height: 300px; line-height: 300px; background: #ff9800;}
        .contents2 {float: left; width: 700px; height: 300px; line-height: 300px; background: #ffa726;}
        .footer {clear: both; width: 1000px; height: 100px; line-height: 100px; background: #ffb74d;}
    </style>
</head>
<body>
    <div id="wrap">
        <div class="header">header</div>
        <div class="nav">nav</div>
        <div class="side">side</div>
        <div class="contents1">contents1</div>
        <div class="contents2">contents2</div> 
        <div class="footer">footer</div>
    </div>
</body>
</html>
```    
  

[layout 04 ![](/assets\Make_Blog\2019-12-19-Makeblog-Website-01-img04.JPG)](/assets\Make_Blog\2019-12-19-Makeblog-Website-01-img04.JPG)  
  
  
## layout 05  
__※__ tip   
[![](/assets/Make_Blog/2019-12-19-Makeblog-Website-01-img05.JPG)](/assets/Make_Blog/2019-12-19-Makeblog-Website-01-img05.JPG)  
  

```css  
<style>  
    #wrap{}
    #header-wrap{width: 100%; height: 100px; background-color: #8d6e63;}
    #banner-wrap{width: 100%; height: 300px; background-color: #a1887f;}
    #content-wrap{width: 100%; height: 500px; background-color: #bcaaa4;}
    #footer-wrap{width: 100%; height: 100px; background-color: #d7ccc8;}
</style>
```  
  

+ 위와 같이 설정할 때 그림과 같이 보이지 않는 기본값 간격이 있다.
+ 이번 레이아웃은 화면 사이즈에 따라 알맞게 보여지는 레이아웃이므로 화면에 가득차게 하기 위해서 기본값을 초기화 해준다.
  + `* { margin: 0; padding: 0;}` : `*`은 전체 선택자
  + 실무에서는 전체선택자를 사용하지 않는다.
+ `width` 값은 기본값이 `100% `이다.
+ 부모와 자식이 같은 값이면 부모에는 값이 없어도 된다.  
  

```html  
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Layout05</title>
    <style>
        * { margin: 0; padding: 0;}
        #wrap {width: 100%; height: 1000px; color:#fff; font-size: 30px; text-align: center; text-transform: uppercase; }
        #header-wrap{width: 100%; height: 100px; background-color: #8d6e63;}
        #banner-wrap{width: 100%; height: 300px; background-color: #a1887f;}
        #content-wrap{width: 100%; height: 500px; background-color: #bcaaa4;}
        #footer-wrap{width: 100%; height: 100px; background-color: #d7ccc8;}

        .header-container {width: 1000px; height: 100px; line-height: 100px; margin: 0 auto; background-color: #3e2723;}
        .banner-container {width: 1000px; height: 300px; line-height: 300px; margin: 0 auto; background-color: #4e342e;}
        .content-container {width: 1000px; height: 500px; line-height: 500px; margin: 0 auto; background-color: #5d4037;}
        .footer-container {width: 1000px; height: 100px; line-height: 100px; margin: 0 auto; background-color: #6d4c41;}
    </style>
</head>
<body>
    <div id="wrap">
        <div id="header-wrap">
            <div class="header-container">header</div>
        </div>
        <div id="banner-wrap">
            <div class="banner-container">banner</div>
        </div>
        <div id="content-wrap">
            <div class="content-container">content</div>   
        </div>
        <div id="footer-wrap">
            <div class="footer-container">footer</div>
        </div>
    </div>
</body>
</html>  
```  
  
[layout 05 ![](/assets\Make_Blog\2019-12-19-Makeblog-Website-01-img06.JPG)](/assets\Make_Blog\2019-12-19-Makeblog-Website-01-img06.JPG)  
   
## layout 06  
`layout 05`를 좀 더 간결하게 작성  

__※__ tip 
+ `inherit`: 부모의 속성을 상속 받을때 사용  

```html  
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <title>layout 06</title>

    <style>
        * {margin: 0;padding: 0;}
        #wrap{}
        #wrap {text-align: center; font-size: 30px; color: #fff;}
        #header {height: 140px; line-height: 140px; background: #ffe1e4;}
        #banner {height: 450px; line-height: 450px; background: #fbd6e3;}
        #contents {height: 950px; line-height: 950px; background: #ead5ee;} 
        #footer {height: 220px; line-height: 220px; background: #d6ebfd;}
        .container {width: 1100px; height: inherit; margin: 0 auto; background: rgba(0,0,0,0.1);}
    </style>
</head>
<body>
    <div id="wrap">
        <div id="header">
            <div class="container">header</div>
        </div>
        <div id="banner">
            <div class="container">banner</div>
        </div>
        <div id="contents">
            <div class="container">contents</div>
        </div>
        <div id="footer">
            <div class="container">footer</div>
        </div>
    </div>
</body>
</html>
```  
  
[layout 06 ![](/assets\Make_Blog\2019-12-19-Makeblog-Website-01-img07.JPG)](/assets\Make_Blog\2019-12-19-Makeblog-Website-01-img07.JPG)  

## layout 07  
layout 06을 세부적으로 나누어 작성  

```html  
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <title>layout 07</title>

    <style>
        /*------------------------- Reset -----------------------------------*/
        * {margin: 0;padding: 0;}

        /*------------------------- Ovarall layout -------------------------*/
        #wrap {text-align: center; font-size: 30px; color: #fff;}
        #header {height: 140px; line-height: 140px; background: #ffe1e4;}
        #banner {height: 450px; line-height: 450px; background: #fbd6e3;}
        #contents {height: 950px; line-height: 950px; background: #ead5ee;} 
        #footer {height: 220px; line-height: 220px; background: #d6ebfd;}
        .container {width: 1100px; height: inherit; margin: 0 auto; background: rgba(0,0,0,0.1);}

        /*------------------------ Detail layout --------------------------*/
        #header-top {height: 70px; line-height: 70px; background: #b2ebf2;}
        #header-nav {height: 70px; line-height: 70px; background: #80deea;}
        #content1 {height: 90px; line-height: 90px; background-color: #26c6da;}
        #content2 {height: 480px; line-height: 480px; background-color: #00bcd4;}
        #content3 {height: 380px; line-height: 380px; background-color: #00acc1;}
        #footer-nav {height: 60px; line-height: 60px; background-color: #0097a7;}
        #footer-info {height: 160px; line-height: 160px; background-color: #00838f;}
    </style>
</head>
<body>
    <div id="wrap">
        <div id="header">
            <div id="header-top">
                <div class="container">header-top</div>
            </div>
            <div id="header-nav">
                <div class="container">header-nav</div>
            </div>
        </div>
        <!-- //header -->
        
        <div id="banner">
            <div class="container">banner</div>
        </div>
        <!-- //banner -->
        
        <div id="contents">
            <div id="content1">
                <div class="container">content1</div>
            </div>
            <div id="content2">
                <div class="container">content2</div>
            </div>
            <div id="content3">
                <div class="container">content3</div>
            </div>
        </div>
        <!-- //contents -->
        
        <div id="footer">
            <div id="footer-nav">
                <div class="container">footer-nav</div>
            </div>
            <div id="footer-info">
                <div class="container">footer-info</div>
            </div>
        </div>
        <!-- //footer -->
    </div>
    <!-- //wrap -->
</body>
</html>
```  
  
[layout 07 ![](/assets\Make_Blog\2019-12-19-Makeblog-Website-01-img08.JPG)](/assets\Make_Blog\2019-12-19-Makeblog-Website-01-img08.JPG)  