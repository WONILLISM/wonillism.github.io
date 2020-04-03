---
title: "[Django] Django ORM과 QuerySets"
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
  
## __쿼리셋(QuerySet)이란?__  
  
전달받은 모델의 객체 목록.  
  
쿼리셋은 데이터베이스로부터 데이터를 읽고, 필터를 걸거나 정렬을 할 수 있다. 
  
### __장고 쉘(shell)__  
로컬 콘솔에서 다음을 입력한다.  
```
python manage.py shell  
```  
실행하면 __파이썬 프롬포트__ 와 비슷한 화면이 나온다.  
  
`Post`모델을 `blog.models`에서 불러온다.  
  
```py  
>>> from blog.models import Post
```   
그러면 아래와 같이 현재 게시된 글 목록을 볼 수 있다.  
  
```py  
Post.objects.all()
<QuerySet [<Post: My first Post!>]>  
```  
  
  
## __객체 생성하기__  
데이터베이스에 새 글 객체를 저장하는 방법  
  
+ `User`는 슈퍼유저로 등록했던 사용자이다. 
+ `User`의 인스턴스를 `me`로 받아와 사용자 이름을 `me`로 바꿔준다.
+ 새로운 게시물을 생성한다.   

```py  
>>> from django.contrib.auth.models import User  
>>> User.objects.all() # User의 모든 오브젝트를 확인하는 방법  
>>> me = User.objects.get(username = 'wonillism')  # 사용자 이름 me로 변경
>>> Post.objects.create(author=me, title = 'Simple title', text = 'Test')  # 새 게시물 생성  
>>> Post.objects.all() # 게시물 확인  
<QuerySet [<Post: My first Post!>, <Post: Simple title>]> # 새 게시물이 생성된 것을 확인 할 수 있다.
```  
  
## __필터링 하기__  
쿼리셋의 중요한 기능 중 하나인 필터링, 예를 들어 `me`이라는 사용자가 작성한 모든 글을 찾고 싶을 때 필터링 할 수 있다.  
  
```py  
>>> Post.objects.filter(author=me)  
<QuerySet [<Post: My first Post!>, <Post: Simple title>, <Post: Hello!!>]>
```  
  
__제목 필터링__  
  
```py  
>>> Post.objects.filter(title__contains = 'title')  
```  
  
__시간 필터링__  
  
`published_date` 게시일 기준으로 목록을 불러올 수 있음  
하지만 파이썬 콘솔에서 추가한 게시물은 아직 보이지 않음.
```py  
>>> from django.utils import timezone  
>>> Post.objects.filter(published_date__lte=timezone.now())    
```  
  
__게시물 게시__  
  
```py  
>>> post = Post.objects.get(title="Simple title")  
>>> post.publish()  
>>> Post.objects.filter(published_date__lte=timezone.now())  
```  
  
__정렬하기__  
  
```py  
>>> post = Post.objects.order_by('create_date') # 날짜별 오름차순 정렬  
>>> post = Post.objects.order_by('-create_date') # 날짜별 내림차순 정렬  
```  
  
__쿼리셋 연결하기__  
  
```py  
>>> Post.objects.filter(published_dtate__lte=timezone.now()).order_by('published_date')  
```  
  
