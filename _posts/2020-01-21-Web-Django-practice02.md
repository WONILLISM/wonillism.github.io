---
title: "[Django] Hello World!"
excerpt: "Hello World를 출력해보자"

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
> Hello World 출력하는 __app__ 을 만들기  
  
## Hello world 출력하기  
__Django__ 프로젝트는 여러개의 __App__ 들로 구성된다. __App__ 은 웹사이트 기능별로 분리해둔 단위라고 생각하면된다.  
  
1. __App__ 만들기
   + 프로젝트 폴더로 이동
   + python manage.py startapp `{앱 이름}`
   + 프로젝트 폴더 안에 `{앱 이름}` 폴더가 생성된다.
2. __Hello World__ 를 출력하는 __index__ 함수 만들기
   + `{앱 이름}` 폴더에서 `views.py`에 다음과 같이 작성한다.  
  
```py  
from django.shortcuts import render
from django.http import HttpResponse

# Create your views here.
def index(request):
    return HttpResponse("Hello World!")
```  
  
3. 앱에 접근할 조건을 지정하는 함수 만들기  
   + {프로젝트 명}/{프로젝트 명} 폴더 안의 `urls.py`를 수정
   + `urls.py`의 `urlpatterns`는 서버에 요청이 들어오면 누가 어떻게 처리할지 담당자를 지정하는 역할을 한다.  
  
```py  
#\mysite\mysite\urls.py
from django.contrib import admin
from django.urls import path,include

urlpatterns = [
    path('', include('app01.urls')), #localhost:8000으로 요청이 들어오면 app.urls로 전달
    path('admin/', admin.site.urls), #app 접속을 위해 include를 사용
]
```  
  
4. 앞서 생성한 index 함수를 실행할 조건을 지정하는 함수 만들기  
```py  
#\mysite\app01\urls.py
from django.conf.urls import path
from . import views #.은 현재 폴더(app01)를 의미

urlpatterns = [
    url(r'^$', views.index), #위의 urls.py와는 달리 include가 없음
]
```  
  
