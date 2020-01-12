---
title: "[코딩야학 7기] 프로젝트 01"
excerpt: "Layout 디자인 하기"

categories:
    - Make_Blog
tags:
    - 코딩야학
    - 생활코딩
    - 프로젝트
    - 블로그
    - blog
    - layout
    - 레이아웃  
use_math: true;
last_modified_at: 2020-01-07
--- 
  
# 코딩야학 7기  
&nbsp; &nbsp; [생활코딩](https://www.youtube.com/channel/UCvc8kv-i5fvFTJBFAk6n1SA) 유투브를 예전에 구독해놓은 적이 있어서 이번에 __코딩야학 7기__ 를 진행한다는 소식을 뒤늦게 알았다. 3일이나 늦은 1/6일에 말이다... 그래도 1주일동안 최대한 할 수 있는 것을 해보고 피드백을 받고싶어서 조만간 할 예정이었던 블로그 만들기를 시작해본다.  
  
## 01. Layout 설계하기  
&nbsp; &nbsp; 우선 내가 만들 블로그가 이런 모양이었으면 좋겠다는 생각으로 포토샵으로 디자인을 구성해보았다.  
  
![Layout Design](/assets/Make_Blog/2020-01-07-Makeblog-Codingyahac-01-img01.JPG)  
지금 블로그와 비슷하지만 __네비게이션__ 메뉴에서 카테고리 부분은 __sidebar__ 에서 볼 수 있고 접었다 펼 수 있게 하고싶다.  
  
현재 사용하고잇는 테마 `minimal_mistakes`를 참고하며 만들고싶지만... 여간 복잡한게 아니다... 차츰차츰 바꿔나가자.  
  


### index.html 파일  
  
```html
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="author" content="WONILLISM">
    <title>Wonillism's Blog</title>
    
    <!-- style -->
    <link rel="stylesheet" type="text/css" href="css/reset.css">
    <link rel="stylesheet" type="text/css" href="css/style.css">
</head>
<body>
    <!-- wrap --> 
    <div id = "wrap">
        <!-- header --> 
        <div id = "header">
                header
        </div>
        <!-- //header --> 
        <!-- content -->
        <div id = "content">
                content
        </div>
        <!-- //content -->
        <!-- sidebar -->
        <div id="sidebar">
                sidebar
        </div>
        <!-- //sidebar -->
        <!-- footer -->
        <div id = "footer">
                footer
        </div>
        <!-- //footer -->

    </div>
    <!-- //wrap -->
</body>
</html>
```  
### style.css 파일    
  
```css
@charset "utf-8";

/* 레이아웃 */
#wrap {width: 100%;}
#header {width: 100%; height: 325px; background: #bf3468; }
#content{width: 100%; height: 800px; background: #832046;}
#footer{width: 100%;height: 200px;background: #300c1a;}
```   
  

### reset.css 파일  
  
```css
@charset "utf-8";

/* 레이아웃 */
@charset "utf-8";

/* 여백 초기화 */
body, div, ul, li, dl, dt, ol, h1, h2, h3, h4, h5, h6, input, fieldset, legend, p, select, table,
th, td, tr, textarea, button, form {margin: 0; padding: 0;}

/* a 링크 초기화 */
a {color: #222; text-decoration: none;}
a:hover {color: #390;}

/* 폰트 초기화 */
body, input, textarea, select, button, table {
    font-family: AppleSDGothicNeo-Regular,'Malgun Gothic','맑은 고딕',dotum,'돋움',sans-serif; 
    color: #222; font-size: 13px; line-height: 1.5;
} 
```  

버튼을 눌렀을 때 사이드바가 접었다 펴지는 기능을 어떻게 넣는지 모르겠다. 좀 더 알아봐야겠다.  
