---
title: "[HTML/CSS] div, span, id, calss"
excerpt: "div와 span의 차이, id와 class의 차이"

categories:
    - WEB
tags:
    - HTML
    - CSS
    - div
    - span
    - id
    - class
use_math: true;
last_modified_at: 2020-02-26
published : false
--- 
> __HTML/CSS__ 공부  
> 개발 언어 : __HTML/CSS__  
> 개발 환경 : __Visual studio Code__  
  
# [HTML/CSS] div와 span, id와 class의 차이는?  
무작정 __blog__ 나 __Youtube__ 를 보면 따라하면서 느꼇던 의문인데 그냥 따라하기만 하다가 확실히 정리해두려고 한다.  

우선 레이아웃의 요소들을 보면   
+ width, height : box 모델의 너비와 높이  
+ display : 화면에 요소가 어떻게 보일지 결정하는 요소  
+ border : box 모델의 테두리
+ margin : box 모델의 마진(요소간 여백)
+ padding : border와 content 사이의 여백
+ border-radius : box 모델의 모서리를 둥글게 처리  
  
## block level, inline level  
박스 모델은 크게 2가지, 블록 레벨과 인라인 레벨로 나뉜다.  
  
+ block-level : 혼자 한 줄을 차지하는 요소(너비는 고정)  
+ inline-level : 줄을 차지하지 않고 화면에 표시되는 content영역 만큼만 차지  
  
## 그룹화 요소 div와 span  
+ __div__  
  + `div`는 __블록(block)__ 요소이며, __인라인(inline)__ 요소와 텍스트를 포함하고 다시 블록 레벨 요소를 포함할 수 있다.
+ __span__  
  + `span`은 __인라인(inline)__ 요소와 텍스트를 포함하지만 블록 레벨 요소를 포함 할 수 없다.  

  
## 선택자 id와 class  
`id`와 `class` 선택자는 특정 요소를 대상으로 스타일을 적용하기 위한 것이다.  
+ __id__
  + __identification: 신분, 신분증명서__ 의 약어로서 __유일성__, 즉, 문서 안에 단 하나만 존재해야한다. 
  + `#`기호를 사용한다.
+ __class__ 
  + 문서 안에 복수의 요소에 스타일을 적용하는 경우에 사용한다.
  + `.`기호를 사용한다.  
  
[![img 01](/assets/HTML-CSS/2020-02-26-Web-html-css-div-span-id-class-img01.PNG)](/assets/HTML-CSS/2020-02-26-Web-html-css-div-span-id-class-img01.PNG)  
  
그림을 보면 `div1`영역에서 `span`들은 줄바꿈을 하지 않고 표시된다. 반면에 `div1`영역 밖의 `span`은 줄바꿈을하고 표시된다.  
  
`class`는 `JAVA`나 `C++`다른 언어에서 하나의 객체로 생각하듯이 `HTML/CSS`에서도 하나의 객체로 생각하면 될 것 같다.  
