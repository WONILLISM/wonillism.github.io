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
