---
title: "[Django] Django 설치하기"
excerpt: "Django를 설치해보자"

categories:
    - WEB
tags:
    - Django
    - 장고
    - Web
    - 웹
    - Web framework
    - 웹 프레임워크
    - tutorial
    - 튜토리얼
use_math: true;
last_modified_at: 2020-01-22
published : false
--- 
> 웹 프레임워크 __Django(장고)__ 공부  
> 개발 언어 : __python 3.8.1__  
> 개발 환경 : __Visual studio Code__  
> 참조 : [장고걸스 튜토리얼](https://tutorial.djangogirls.org/ko/)   
  
직접 블로그를 만들기위해 __Django__ 를 공부해보자.  
  
# __Django(장고)란?__  
[![장고](/assets/Web/Django/Django.jpeg)](/assets/Web/Django/Django.jpeg)  
Django(/dʒæŋɡoʊ/ jang-goh/쟁고/장고)는 파이썬으로 만들어진 무료 오픈소스 웹 애플리케이션 프레임워크(web application framework)이다. 쉽고 빠르게 웹사이트를 개발할 수 있도록 돕는 구성요소로 이루어진 웹 프레임워크이다.  
  
파이썬, 장고, VS code(visual studio code)를 미리 설치 해놓아야한다. 
설치법이 궁금하다면 구글링을 해보자. 구글구글  
  
## __Django 설치하기__  
### __가상환경(Virtual Environment)__
Virtualenv(= Virtual Environment)는 프로젝트 기초 전부를 Python/Django 와 분리해준다. 즉, 웹사이트가 변경되어도 개발 중인 것에 영향을 미치지 않는다.  
+ command-line  
```
$ python -m venv myvenv
```  
  
### __장고 설치하기__  
pip 최신버전 설치하기
```
python -m pip install --uptrade pip
```  
  
### __장고 프로젝트 만들기__  
장고에서는 디렉토리와 파일명이 매우 중요하다. 파일명을 마음대로 변경해서도 안되고 다른 곳으로 옮겨서도 안된다. 장고는 중요한 것들을 찾을 수 있게 특정 구조를 유지해야 한다.  
`django-admin.py` : 스크립트로 디렉토리와 파일들을 생성한다. 스크립트 실행 후에는 아래와 같은 새로운 디렉토리 구조를 볼 수 있다.  
```  
djangogirls
├───manage.py
└───mysite
        settings.py
        urls.py
        wsgi.py
        __init__.py
```  

`manage.py` : 사이트 관리를 도와주는역할, 이 스크립트로 다른 설치 작업 없이 컴퓨터에서 웹 서버를 시작할 수 있다.  
  
`settings.py` : 웹사이트 설정이 있는 파일이다.  
  
`urls.py` : `urlesolver`가 사용하는 패턴 목록을 포함하고 있다.  

### __설정 변경__  
  
mysite/settings.py
```py
TIME_ZONE = 'Asia/Seoul'

STATIC_URL = '/static/'
STATIC_ROOT = os.path.join(BASE_DIR, 'static')
  
ALLOWED_HOSTS = ['127.0.0.1', '.pythonanywhere.com']  
```  

### __데이터베이스 설정하기__  
   + `python manage.py migrate`
   + `python manage.py runserver`
   + https://127.0.0.1:8000 으로 접속  
  