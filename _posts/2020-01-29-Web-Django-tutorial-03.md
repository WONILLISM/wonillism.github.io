---
title: "[Django] Django 관리자"
excerpt: "Django 관리자를 만들어 포스팅 해보기"

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
last_modified_at: 2020-01-29
--- 
> 웹 프레임워크 __Django(장고)__ 공부  
> 개발 언어 : __python 3.8.1__  
> 개발 환경 : __Visual studio Code__  
> 참조 : [장고걸스 튜토리얼](https://tutorial.djangogirls.org/ko/)   
  
직접 블로그를 만들기위해 __Django__ 를 공부해보자.  
  
## __장고 관리자__  
관리자 화면을 한국어로 바꾸기  
    + `settings.py` -> `LANGUAGE_CODE = 'ko'`로 바꾸기  
  
`blog/admin.py` 아래와 같이 수정    
```py  
from django.contrib import admin
from .models import Post

admin.site.register(Post)
```  
  
모든 권한을 가지는 `superuser` 생성  
`python manage.py createsuperuser`  
  
```
Username: admin
Email address: admin@admin.com
Password:
Password (again):
```  
`superuser` 설정  

`http://127.0.0.1/8000/admin`에 접속해서 로그인을 하면 다음과 같은 화면이 보인다.  
[![장고 admin](/assets/Web/Django/2020-01-29-Web-Django-tutorial-03-img01.PNG)](/assets/Web/Django/2020-01-29-Web-Django-tutorial-03-img01.PNG)  
  
`Post`를 추가하고 변경할 수 있다.  
