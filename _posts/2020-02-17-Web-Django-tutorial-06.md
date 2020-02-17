---
title: "[Django] 장고 템플릿"
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
last_modified_at: 2020-02-17
--- 
> 웹 프레임워크 __Django(장고)__ 공부  
> 개발 언어 : __python 3.8.1__  
> 개발 환경 : __Visual studio Code__  
> 참조 : [장고걸스 튜토리얼](https://tutorial.djangogirls.org/ko/)   
  
직접 블로그를 만들기위해 __Django__ 를 공부해보자.  
  
## __템플릿 동적 데이터__  
블로그 글은 각각 다른 장소에 조각조각 나누어져있다. `Post` 모델은 `models.py` 파일에, `post_list` 모델은 `views.py` 파일에 존재한다.  
  
뷰(View)는 모델과 템플릿을 연결하는 역할을 한다. `post_list`를 뷰에서 보여주고 이를 템플릿에 전달하기 위해서는 모델을 가져와야한다. 일반적으로 ___뷰___ 가 ___템플릿___ 에서 모델을 선택하도록 만들어야 한다.  

`blog/view.py`에 `from .models import Post`를 추가한다.
```py  
from django.shortcuts import render
from .models import Post

# Create your views here.
def post_list(request):
    return render(request, 'blog/post_list.html', {})

```
  
`from` 다음에 있는 .은 현재 디렉토리(폴더) 또는 애플리케이션을 의미한다. 동일한 디렉토리 안에 `veiw.py`, `models.py` 파일이 존재하기 때문에 확장자를 붙이지 않아도 내용을 가져올 수 있다.  
  
`Post`모델에서 블로그 글을 가져오기 위해서는 `쿼리셋(QuerySet)`이 필요하다.  
  
## __쿼리셋(QuerySet)__  
블로그 글을 `published_date`기준으로 정렬해보다.  
> 이 과정을 진행하는 도중에 python manage.py 를 실행하려니 아래와 같은 오류가 발생했다.  
> __django.core.exceptions.ImproperlyConfigured: Application labels aren't unique, duplicates: contenttypes__  
> 구글링을 해도 죄다 영문이고... 대충 해석해서 알아봐도 뭐가 뭔지 잘 모르겠고... 그래서 좀 더 자세히 읽어보았다.  
> 문제는 settings.py 안의 INSTALLED_APPS에 'django.contrib.contenttypes' 이게 중복되어잇었다.. 이유가 뭐지..?  
  
`blog/views.py`를 아래와 같이 수정한다.  
```py  
from django.shortcuts import render
from django.utils import timezone
from .models import Post


# Create your views here.
def post_list(request):
    posts = Post.objects.filter(published_date__lte=timezone.now()).order_by('published_date')
    return render(request, 'blog/post_list.html', {})
```  
아직 `posts`파일이 적용되지 않았지만 나중에 `posts`파일로 `QuerySet`을 템플릿 컨텍스트에 전달하기 위해 만들어둔다.  
`render`함수에는 매개변수 `request`(사용자가 요청하는 모든 것))와 `blog/post_list.html` 템플릿이 있다.  
`return render(request, 'blog/post_list.html', {'posts': posts})` 로 수정하여 템플릿을 사용하기 위한 매개변수 `post`를 추가한다.  
  
```py  
from django.shortcuts import render
from django.utils import timezone
from .models import Post


# Create your views here.
def post_list(request):
    posts = Post.objects.filter(published_date__lte=timezone.now()).order_by('published_date')
    return render(request, 'blog/post_list.html', {})
```  
  
## __장고 템플릿__  
템플릿 태그는 정적인 `HTML`에 동적인 `python`을 `HTML`로 바꾸어주어 빠르고 쉽게 동적인 웹사이트로 만들 수 있게 도와준다.  
  
## __post 목록 템플릿 보여주기__  
  
`blog/templates/blog/post_list.html`을 아래와 같이 수정해준다.  
  
```html  
<!DOCTYPE html>
<html>
    <head>
        <title>Wonillism blog</title>
    </head>
    <body>
        <div>
            <h1><a href="">Wonillism Blog</a></h1>
        </div>

        {% for post in posts %}
            {{post}}
            <div>
                <p>published: {{ post.published_date }}</p>
                <h1><a href="">{{ post.title}}</a></h1>
                <p>{{ post.test|linebreaksbr}}</p>
            </div>
        {% endfor %}

    </body>
</html>

```  
`{% for %}, {% endfor %}`을 이용하여 모든 포스트를 보여준다.  

[![](/assets/web/Django/2020-02-17-Web-Django-tutorial-05-img01.png)](/assets/web/Django/2020-02-17-Web-Django-tutorial-05-img01.png)  
  
이제 슬슬 블로그의 모양이 나오는 것 같다!