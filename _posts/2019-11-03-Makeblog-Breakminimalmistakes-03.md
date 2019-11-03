---
title: "[Making_Blog] minimal-mistakes 뿌시기 03"
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
지킬에서 게시물은 크게 post와 page로 구분된다. 그래서 폴더도 _post와 _page로 나뉘는데 _post에는 내가 블로그에 올릴 포스트들이 저장되는 곳이다. post파일들은 날짜 기반(ex  yyyy-mm-dd-post-title.md)으로 작성된다. _page에는 포스팅을 제외한 특정 페이지를 보여줄 페이지 파일들이 저장되는 곳이다.  
  
## page 글 등록하기  
minimal-mistakes theme 초기에는 _pages 폴더가 존제하지 않는다. _pages 폴더를 만들고 그 안에 들어갈 404.md, about.md, category-archive.md, tag-archive.md를 작성해보자.  
  
__about.md__  
```md
---  
title: "About WONILLISM's Blog"
permalink: /about/
layout: single
header:
  overlay_image: /assets/Images/main-teaser.jpg
  overlay_filter: 0.5
---
## WONILLISM.github.io 블로그
```  
블로그에 대한 설명을 하는 페이지이다.  
`---` ~ `---`에 들어가는 내용은 yaml front matter 라고 불리는데 작성할 글(post, page 등)에 대한 머릿말이라고 생각하면된다.  
jekyll 홈페이지에 머릿말에 관해서 자세히 설명되어있다. -> [Jekyll - 머릿말](https://jekyllrb-ko.github.io/docs/frontmatter/)  
간단히 설명하자면 
  + `title`은 브라우저의 머릿말과 그리고 페이지의 제목으로 이용된다.  
  + `permalink`는 이 페이지에 대한 경로라고 생각하면된다.  
  + `layout`은 이 글에 사용될 레이아웃이라고 생각하면되는데, minimal-mistakes 테마에서는 크게 `single`과 `splash`로 주어진다. 
  + `header`에 대한 설명은 아래에서 하겠다.  

  
__404.md__  
```md
---
title: "Page Not Found"
excerpt: "Page not found. Your pixels are in another canvas."
permalink: /404.html
author_profile: false
---  
요청하신 페이지를 찾을 수 없습니다.

<script>
  var GOOG_FIXURL_LANG = 'en';
  var GOOG_FIXURL_SITE = 'https://wonillism.github.io'
</script>
<script src="https://linkhelp.clients.google.com/tbproxy/lh/wm/fixurl.js">
</script>
```  
잘못된 경로 혹은 존재하지 않는 페이지로 들어왔을 때 보여질 페이지이다.  
  
__category-archive.md__  

```md  
---
title: "Posts by Category"
layout: categories
permalink: /categories/
author_profile: true
---
```  
minimal-mistakes 가이드는 상단 navigation 메뉴에 들어갈 예시를 category별로 모여있는 페이지, tag별로 모여있는 페이지, about페이지를 주는데, 포스트를 작성할 때 yaml 머릿말에 카테고리를 분류할 수 있는데, 그때 분류된 카테고리 별로 포스트를 보여주는 페이지이다.  
`author_profile`은 왼쪽에 보여질 블로그 저자 프로필을 켜고 끌 수 있다. 작성하지 않는다면 `false`가 초기값이다.  

__tag-archive.md__  
```md
---  
title: "Posts by Tag"
permalink: /tags/
layout: tags
author_profile: true
---  
```  
tag 별로 보여주기 위한 페이지  
