---
title: "[Making_Blog] minimal-mistakes 뿌시기 02"
excerpt: "지킬 테마 minimal-mistakes를 알아보자."

categories:
    - Make_Blog
tags:
    - Blog  
    - 블로그 만들기
    - jekyll
    - github blog
    - 깃헙 블로그
    - jekyll theme
    - 지킬 테마
    - minimal-mistakes  
last_modified_at: 2019-11-02
published : false
---  
## 블로그 기본 설정  
jekyll의 기본 구성을 설정할 수 있는 `_config.yml`파일은 전체 사이트에 영향을 준다.  
`_config.yml`파일 안에 이 테마의 개발자가 친절하게 주석을 달아놨다.  
사이트 세팅, SNS주소 설정, 구굴 애널리틱스 설정, 왼쪽에 표시될 블로그 주인에 대한 설명 설정 등등 기본적으로 세팅할 수 있도록 해놓았다.   
  
## 기본 구성  
__스킨 설정__  
기본적으로 제공되는 스킨중 마음에 드는 스킨으로 쉽게 변경할 수 있다.  
```yml
minimal_mistakes_skin    : "default" # "air", "aqua", "contrast", "dark", "dirt", "neon", "mint", "plum", "sunrise"
```  

__사이트 설정__   

```yml  
# Site Settings
locale                   : "ko-KR"  # 사이트 기본 언어 선언
title                    : "WONILLISM's Blog" # title에 표시될 부분
title_separator          : "-"
subtitle                 : # 사이트 제목 아래 표시되는 사이트 태그 라인  
name                     : "WONILLISM"
description              : "나의 공부 스택"
url                      : "https://WONILLISM.github.io"
baseurl                  : # 서브경로가 있는 경우 기재
repository               : https://github.com/wonillism # GitHub username/repo-name e.g. "mmistakes/minimal-mistakes"
teaser                   :  # 티저 이미지가 뭐지..? , e.g. "/assets/images/500x300.png"
logo                     : # 마스트헤드 부분 제목 옆에 로고 이미지, e.g. "/assets/images/88x88.png"
masthead_title           : # overrides the website title displayed in the masthead, use " " for no title
# breadcrumbs            : false # true, false (default)
words_per_minute         : 200
```  
  
__사이트 저자 소개__  
  
```yml  
# Site Author
author:
  name             : "Park Won Il"
  avatar           : # path of avatar image, e.g. "/assets/images/bio-photo.jpg"
  bio              : "늦깎이 개발자 지망생"
  location         : "South Korea"
  email            :
  links:
    - label: "Email"
      icon: "fas fa-fw fa-envelope-square"
      url: wonillism@gmail.com
    #- label: "Website"
    #  icon: "fas fa-fw fa-link"
      # url: "https://your-website.com"
    #- label: "Twitter"
    #  icon: "fab fa-fw fa-twitter-square"
      # url: "https://twitter.com/"
    #- label: "Facebook"
    #  icon: "fab fa-fw fa-facebook-square"
      # url: "https://facebook.com/"
    - label: "GitHub"
      icon: "fab fa-fw fa-github"
      url: "https://github.com/WONILLISM/WONILLISM.github.io"
    #- label: "Instagram"
    #  icon: "fab fa-fw fa-instagram"
      # url: "https://instagram.com/"

```  
사이트 좌측에 기본적으로 사이트 저자 소개 항목이 존재한다. 이 부분을 원하지 않는다면 간단한 설정으로 안보이게할 수 있다.  
나는 상단에 있는 메뉴바를 이 사이트 저자 소개 부분으로 옮기고 싶은데 방법을 모르겠다. 사실 이거하려고 이 포스팅을 하고 있기도 하다...  
  
__사이트 Footer__  
사이트 맨 아래 부분에 표시되는 영역의 설정을 의미한다. 나는 깃허브 주소만 올려놓았다.  
  

```yml  
# Site Footer
footer:
  links:
    #- label: "Twitter"
    #  icon: "fab fa-fw fa-twitter-square"
      # url:
    #- label: "Facebook"
    #  icon: "fab fa-fw fa-facebook-square"
      # url:
    - label: "GitHub"
      icon: "fab fa-fw fa-github"
      url: https://github.com/wonillism/wonillism.github.io
      # url:
    #- label: "GitLab"
    #  icon: "fab fa-fw fa-gitlab"
      # url:
    #- label: "Bitbucket"
    #  icon: "fab fa-fw fa-bitbucket"
      # url:
    #- label: "Instagram"
    #  icon: "fab fa-fw fa-instagram"
      # url:
```  
  
__블로그 표시 방법 설정__  
초기 블로그 표시방법 설정 부분이다.  
```yml
# Outputting
permalink: /:categories/:title/
paginate: 5 # 한 번에 보여지는 포스트 수
paginate_path: /page:num/
timezone: # https://en.wikipedia.org/wiki/List_of_tz_database_time_zones
```  
  
__기본 page 설정__  
post를 별도의 페이지로 설정해놨지만, 보여지는 페이지에 대한 기본 설정을 하는 부분이다.    
  
  
```yml
# Defaults
defaults:
  # _posts
  - scope:
      path: ""
      type: posts
    values:
      layout: single
      author_profile: true
      read_time: true
      comments: true # true
      share: true
      related: true


  # _pages
  - scope:
      path: ""
      type: pages
    values:
      layout: single
      author_profile: true
      read_time: false
      comments: false
      share: true
      related: false  

```