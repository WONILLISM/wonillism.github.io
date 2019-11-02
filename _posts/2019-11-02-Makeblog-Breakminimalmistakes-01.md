---
title: "[Making_Blog] minimal-mistakes 뿌시기 01"
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
    - github blog
last_modified_at: 2019-09-27
---
![](assets/../../assets/Make_Blog/2019-11-02-Makeblog-Breakminimalmistakes-01-img01.jpg)  
깃헙 블로그를 좀 더 내 입맛에 맞게, 좀 더 블로그 답게 꾸미고 싶었다. 그동안의 포스팅도 포기하며... 계속해서 구글링을하고 다른 블로그로 갈아탈까 고민하고..  
애초에 내가 html/css를 공부를 했으면 이런 시행착오도 덜 했을 것이다. 아니면 영어를 잘하던가...  
하지만 이왕 깃헙 블로그를 시작했으니 끝을 보자는 생각으로 포스팅을 시작한다.  
  
# minimal-mistakes 
__minimal-mistakes__ 는 [Michael Rose](https://mmistakes.github.io/minimal-mistakes/about/)라는 사람이 만든 jekyll 테마이다. 조금씩 알아볼수록 진짜 대단한 사람 같다. 몇 년 전부터 만들어진 테마인데 아직까지도 업데이트를 하며 __Git issue__ 에 꼬박꼬박 답변도 달아주고 매우 활성화되어있다. 깃헙 블로그를 버리지 못한 가장 큰 이유이기도 하다.  
제대로 알지는 못하지만 구조자체가 매우 체계적이고 섬세하다. 그래서 더 알아보고싶은 맘이 생겼다.  

배포되고있는 [Quick-Start Guide](https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/)를 꼼꼼히 읽으며 연구해보자.  
  

참고 :
 + <https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/>  
 + https://devinlife.com/howto/

## 구조  
```  
inimal-mistakes
├── _data                      # data files for customizing the theme
|  ├── navigation.yml          # main navigation links
|  └── ui-text.yml             # text used throughout the theme's UI
├── _includes
|  ├── analytics-providers     # snippets for analytics (Google and custom)
|  ├── comments-providers      # snippets for comments
|  ├── footer                  # custom snippets to add to site footer
|  ├── head                    # custom snippets to add to site head
|  ├── feature_row             # feature row helper
|  ├── gallery                 # image gallery helper
|  ├── group-by-array          # group by array helper for archives
|  ├── nav_list                # navigation list helper
|  ├── toc                     # table of contents helper
|  └── ...
├── _layouts
|  ├── archive-taxonomy.html   # tag/category archive for Jekyll Archives plugin
|  ├── archive.html            # archive base
|  ├── categories.html         # archive listing posts grouped by category
|  ├── category.html           # archive listing posts grouped by specific category
|  ├── collection.html         # archive listing documents in a specific collection
|  ├── compress.html           # compresses HTML in pure Liquid
|  ├── default.html            # base for all other layouts
|  ├── home.html               # home page
|  ├── posts.html              # archive listing posts grouped by year
|  ├── search.html             # search page
|  ├── single.html             # single document (post/page/etc)
|  ├── tag.html                # archive listing posts grouped by specific tag
|  ├── tags.html               # archive listing posts grouped by tags
|  └── splash.html             # splash page
├── _sass                      # SCSS partials
├── assets
|  ├── css
|  |  └── main.scss            # main stylesheet, loads SCSS partials from _sass
|  ├── images                  # image assets for posts/pages/collections/etc.
|  ├── js
|  |  ├── plugins              # jQuery plugins
|  |  ├── vendor               # vendor scripts
|  |  ├── _main.js             # plugin settings and other scripts to load after jQuery
|  |  └── main.min.js          # optimized and concatenated script file loaded before </body>
├── _config.yml                # site configuration
├── Gemfile                    # gem file dependencies
├── index.html                 # paginated home page showing recent posts
└── package.json               # NPM build scripts
```  
위와 같은 구성인데 아무리 봐도 잘 모르겠다.  
  
## 구성  
jekyll의 기본 구성을 설정할 수 있는 `_config.yml`파일은 전체 사이트에 영향을 준다.  
`_config.yml`파일 안에 이 테마의 개발자가 친절하게 주석을 달아놨다.  
사이트 세팅, SNS주소 설정, 구굴 애널리틱스 설정, 왼쪽에 표시될 블로그 주인에 대한 설명 설정 등등 기본적으로 세팅할 수 있도록 해놓았다.   
  
[![](/assets/Make_Blog/2019-11-02-Makeblog-Breakminimalmistakes-01-img02.jpg)](/assets/Make_Blog/2019-11-02-Makeblog-Breakminimalmistakes-01-img02.jpg)
