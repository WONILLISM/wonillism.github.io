---
title: "[Django] Django urls"
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
last_modified_at: 2020-02-15
published : false
--- 
> 웹 프레임워크 __Django(장고)__ 공부  
> 개발 언어 : __python 3.8.1__  
> 개발 환경 : __Visual studio Code__  
> 참조 : [장고걸스 튜토리얼](https://tutorial.djangogirls.org/ko/)   
  
직접 블로그를 만들기위해 __Django__ 를 공부해보자.  
  
## __장고 urls__  
`mysite/urls.py` 파일을 열어보면 아래와 같다.  
```py  
from django.contrib import admin
from django.urls import path

urlpatterns = [
    path('admin/', admin.site.urls),
]
```  
위 `path`의 의미는 장고는 `admin/`로 시작하는 모든 __URL__ 을 __view__ 와 대조해 찾아낸다. 무수히 많은 __URL__ 이 `admin URL`에 포함될 수 있어 일일이 모두 쓸 수 없기 때문에 정규표현식을 사용한다.  
  
`mysite/urls.py`파일을 깨끗한 상태로 유지하기 위해 `blog`에플리케이션에서 메인 `mysite/urls.py` 파일로 url들을 가지고 올 것이다.  
  
`mysite/urls.py`를 아래와 같이 수정해준다.  
```py  
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('blog.urls')),
]
```  
  
이제 로컬호스트(127.0.0.1:8000)로 들어오는 모든 접속 요청을 `blog.urls`로 전송해 추가 명령을 찾는다. 이를 위해 `blog/urls.py`를 아래와 같이 생성한다.  

```py  
from django.urls import path
from .import views

urlpatterns = [
    path('', views.post_list, name='post_list'),
]
```  
  
위의 과정을 작성한 후 로컬서버를 작동시켜보면 다음과 같은 오류가 나온다.  
[![](/assets/Web/Django/2020-02-15-Web-Django-tutorial-04-img01.png)](/assets/Web/Django/2020-02-15-Web-Django-tutorial-04-img01.png)  
  
## HTML 시작하기   
위에서 템플릿이 존제하지 않는다는 에러가 났다. 템플릿이란 뭘까?  
  
+ 템플릿이란?
  + 서로 다른 정보를 일정한 형태로 표시하기 위해 재사용 가능한 파일을 말한다. 이를 표현하기위해 장고는 템플릿 양식을 HTML을 사용한다.  
  
```
blog
└───templates
 └───blog
```  
우선 `blog`하위 폴더에 `templates/blog` 폴더를 만들자.  
똑같은 `blog` 폴더를 하나 더 만드는 이유는 나중에 구조가 복잡해졌을 때 좀 더 쉽게 찾기 위해 사용하는 관습적인 방법이다.  
  
`blog/templates/blog`폴더에 `post_list.html`파일을 하나 생성한다.  
이제 로컬호스트를 실행하면 비어있는 페이지 하나가 작동한다.  

  
