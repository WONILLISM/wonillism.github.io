---
title: "[Django] Django 모델"
excerpt: "블로그 내 모든 포스트를 저장하는 부분 만들기"

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
last_modified_at: 2020-01-26
--- 
> 웹 프레임워크 __Django(장고)__ 공부  
> 개발 언어 : __python 3.8.1__  
> 개발 환경 : __Visual studio Code__  
> 참조 : [장고걸스 튜토리얼](https://tutorial.djangogirls.org/ko/)   
  
직접 블로그를 만들기위해 __Django__ 를 공부해보자.  
  
## __객채(Object)__  
블로그를 객체지향설계 해보자.  
객체지향설계란 현실에 존재하는 것을 속성과 행위로 나타낸 것이다.  
속성 = `객체속성(properties)`, 행위 =  `메서드(methods)`  
  
```
Post(게시글)
--------
title(제목)
text(내용)
author(글쓴이)
created_date(작성일)
published_date(게시일)
```  
  
## __어플리케이션 만들기__  
가상환경이 켜져있는 상태에서 아래 커맨드를 입력한다.  
`python manage.py startapp blog`  
애플리케이션을 생성한 후 장고에게 사용한다고 알려줘야하는데 이 역할을 하는 파일이 `mysite/settings.py`이다.  
  
`mysite/settings.py`에 `INSTALLED_APPS`에 `blog`를 추가한다.  
  
## __블로그 글 모델 만들기__  
모든 `Model` 객체는 `blog/models.py`에 선언하여 모델을 만든다.  
`blog/models.py`에 모든 내용을 삭제한 후 다음 코드를 입력한다.  
  
```py  
from django.conf import settings
from django.db import models
from django.utils import timezone


class Post(models.Model):
    author = models.ForeignKey(settings.AUTH_USER_MODEL, on_delete=models.CASCADE)
    title = models.CharField(max_length=200)
    text = models.TextField()
    created_date = models.DateTimeField(
            default=timezone.now)
    published_date = models.DateTimeField(
            blank=True, null=True)

    def publish(self):
        self.published_date = timezone.now()
        self.save()

    def __str__(self):
        return self.title
```  
  
__※코드분석__  
+ `class Post(models.Model):`
  + 모델을 정의
  + `class` : 객체를 정의 
  + `Post` : 모델의 이름(클래스의 이름의 첫 글자는 항상 대문자)
  + `models` : `Post`가 장고 모델임을 의미 -> 이 코드로 인해 장고는 `Post`가 데이터베이스에 저장되어야 한다고 인식  
+ 속성 정의  
  + `models.CharField` : 글자 수가 제한된 텍스트를 정의할 때 사용(ex. 글 제목)  
  + `models.TextField` : 글자 수에 제한이 없는 긴 텍스트를 정의 할 때 사용  
  + `models.DateTimeField` : 날짜와 시간을 의미  
  + `models.ForeignKey` : 다른 모델에 대한 링크를 의미  
  
장고 공식 문서 참조    
<https://docs.djangoproject.com/en/2.0/ref/models/fields/#field-types)>  
  
## __데이터베이스에 모델을 위한 테이블 만들기__  
1. 장고 모델에 몇가지 변화를 알려주기
   + `python manage.py makemigrations blog` 입력 
2. 실제 데이터베이스에 모델 추가 반영하기  
   + `python manage.py migrate blog` 입력  


