---
title: "[Django] 프로젝트 생성하기"
excerpt: "장고 프로젝트를 만들어보자."

categories:
    - WEB
tags:
    - Django
    - 장고
    - Web
    - 웹
    - Web framework
    - 웹 프레임워크
use_math: true;
last_modified_at: 2020-01-21
--- 
> 웹 프레임워크 __Django(장고)__ 공부  
> 개발 언어 : __python__  
> 개발 환경 : __Visual studio Code__  
  
직접 블로그를 만들기위해 __Django__ 를 공부해보자.  
  
# __Django(장고)란?__  
[![장고](/assets/Web/Django/Django.jpeg)](/assets/Web/Django/Django.jpeg)  
Django(/dʒæŋɡoʊ/ jang-goh/쟁고/장고)는 파이썬으로 만들어진 무료 오픈소스 웹 애플리케이션 프레임워크(web application framework)이다. 쉽고 빠르게 웹사이트를 개발할 수 있도록 돕는 구성요소로 이루어진 웹 프레임워크이다.  
  
파이썬, 장고, VS code(visual studio code)를 미리 설치 해놓아야한다. 
설치법이 궁금하다면 구글링을 해보자. 구글구글  
  
## __Django 프로젝트 만들기__  
1. __Django 프로젝트 생성__  
   + 프로젝트를 만들고자 하는 폴더로 이동
   + 터미널에 django-admin startproject {프로젝트 이름} 입력
2. __Django 서버 실행__  
   + {프로젝트 이름} 폴더로 이동
   + 터미널에 python manage.py runserver 입력
3. __Django 서버 접속__
   + 주소창에 127.0.0.1:8000 or localhost:8000 입력
   + 서버 중단은 `ctrl` + `c`를 누르면 된다.  
  
