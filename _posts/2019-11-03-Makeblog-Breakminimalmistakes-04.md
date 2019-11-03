---
title: "[Making_Blog] minimal-mistakes 뿌시기 04"
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
last_modified_at: 2019-11-04
---  
### 블로그 메뉴 만들기  
이전의 포스트에서 만든 page들을 상단 메뉴에 링크를 걸어보자.  
`_data/navegation.yml` 파일을 보면 아래와 같다.  
```yml  
# main links
main:
  - title: "Categories"
    url: /categories/
  - title: "Tags"
    url: /tags/
  - title: "About"
    url: /about/
  #   url: https://mmistakes.github.io/minimal-mistakes/about/
  # - title: "Sample Posts"
  #   url: /year-archive/
  # - title: "Sample Collections"
  #   url: /collection-archive/
  # - title: "Sitemap"
  #   url: /sitemap/
```  
초기값은 주석처리된 부분과 같이 되어있는데, 나는 이전 포스트에서 만든 페이지들을 이용하여 `Categories`, `Tags`, `About`링크를 만들어보았다.  
상단의 메뉴는 메인 메뉴로 `main`이라고 정의되어있다. 그 아래 만들어줄 링크의 이름과 `url`을 설정해주면되는데 이 `url`은 이전 포스트에서 만든 page yaml 머릿말에 정의해 준 permalink에 입력했던 이름을 쓰면된다.  

  
처음 이 <minimal-mistakes 뿌시기> 포스팅을 하게된 이유가 메뉴바의 위치와 방식을 바꾸고싶어서였다. 이 `navigation.yml`부분을 좀 건드리면 될 것 같다고 생각했었는데 __Guide__ 에도 원하는 방식으로 나와있지 않고 구글링을해도 안나온다.. 그래서 minimal-mistakes 개발자의 깃허브에 가서 `issue`로 질문을 남겨놓았다. 돌아오는 답변은................  
[![img1](/assets/Make_Blog/2019-11-03-Makeblog-Breakminimalmistakes-04-img01.jpg)](/assets/Make_Blog/2019-11-03-Makeblog-Breakminimalmistakes-04-img01.jpg)  
  
css와 javascript를 작성하여 바꿔야한답니다... 앞으로 공부해야할게 하나 더 생겼다.
