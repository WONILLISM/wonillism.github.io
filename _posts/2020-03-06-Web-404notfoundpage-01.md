---
title: "[WEB] 404 page 만들기 01"
excerpt: "404 page 만들기 HTML 구조"

categories:
    - WEB
tags:
    - javascript
    - 자바스크립트
    - vanilla JS
    - vanilla
    - html
    - css
    - 404 page
    - 웹 개발
    - 프론트 엔드
    - front end
use_math: true;

last_modified_at: 2020-03-06
--- 
> __WEB__ 공부  
> 개발 언어 : __HTML, CSS, Javascript__  
> 개발 환경 : __Visual studio Code__  

## __구조(Structure)__  

```
body
├───nav
│       ├nav-HOME
│       └nav-contactus
├───main
│       ├message-404
│       ├collage-404
│       └color-search
└───footer
        └search
```

## __HTML__  
`index.html (body 이하)`  
```html 
<body>
    <!-- nav -->
    <nav>
        <a class="nav-HOME" href="https://wonillism.github.io">Home</a>
        <span>
            <a class="nav-contactus">Contact us</a>
        </span>
    </nav>

    <!-- main -->
    <main>
        <section class="message-404">
            <h1>Whoops, that page is gone.</h1>
            <p>While you're here, feast your eyes upon these trantalizing popular designs matching the color <a
                    id="color-choice"></a>.</p>
        </section>
        <section class="collage-404">
            <h1>404</h1>
            <div class="collage-404-colors"></div>
        </section>
        <section class="color-search">
            <div>
                <input class="color-range" type="range" min="0" max="100" value="75" title="Drag me, baby.">
            </div>
        </section>
    </main>

    <!-- footer -->
    <footer>
        <form id="search">
            <div class="input">
                <svg class="input-icon" width="16" height="16" viewBox="0 0 16 16" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <g clip-path="url(#clip0)">
                        <circle cx="6.75" cy="6.75" r="5.75" stroke="black" stroke-width="2" />
                        <path d="M11.5 11.5L15.5 15.5" stroke="black" stroke-width="2" />
                    </g>
                </svg>
                <input type="search" name="q" value="" placeholder="Search color" name="q">
            </div>
        </form>
    </footer>
    <!--  script  -->  
    <script src="src/index.js"></script>  
</body>  
```

+ __`article`, `section`, `div` 차이__   
__article__ : 독립적이고 홀로 설 수 있는 내용 (블로그 글, 포럼 글, 뉴스 기사 등)  
__section__ : 내용이 서로 연관되어 있는 문서를 구분할 때  
__div__ : 의미적으로 관계가 없을 때(오직 내용을 묶는 역할)  

+ __`form` tag__   

  __사용자 입력을 수집__ 하여 서버에 전달하는데 사용

+ __input tag__  

|   속성    |     속성값     |                            설명                             |
| :-------: | :------------: | :---------------------------------------------------------: |
|   type    |     button     |    text 입력(text input) 위 __한 줄__의 입력 필드를 정의    |
|           |    checkbox    |                       checkbox를 정의                       |
|           |     color      |            색상을 포함해야하는 입력 필드에 사용             |
|           |      date      |       사용자가 날짜를 포함해야 하는 입력 필드에 사용        |
|           | datetime-local |  사용자가 날짜와 시간을 (시간대 없이) 선택할 수 있게 해줌   |
|           |      file      |             사용자가 파일을 선택할 수 있게 해줌             |
|           |     hidden     |                                                             |
|           |     image      |                                                             |
|           |     month      |           사용자가 월, 년도를 선택할 수 있게 해줌           |
|           |     number     |             숫자 값을 포함하는 입력 필드에 사용             |
|           |    password    |     __password__ 필드 정의 (별표 혹은 동그라미로 표시)      |
|           |     radio      |             라디오 버튼(__radio button__) 정의              |
|           |     range      | 값이 범위 안에 있어야하는 입력 필드에 사용(슬라이드 컨트롤) |
|           |     reset      |             초기화 버튼(__reset button__) 정의              |
|           |     search     |                      검색 필드에 사용                       |
|           |     submit     |              제출 버튼(__submit button__) 정의              |
|           |      tel       |                  전화 번호 입력 필드 정의                   |
|           |      text      |                    텍스트 입력 필드 정의                    |
|           |      time      |             사용자가 시간을 선택할 수 있게 해줌             |
|           |      url       |          __URL__ 주소를 포함하는 입력 필드에 사용           |
|           |      week      |          사용자가 주와 년도를 선택할 수 있게 해줌           |
| disabled  |                |              입력 필드를 사용하지 못하게 정의               |
|    max    |                |                입력 필드에 대한 최대값 정의                 |
| maxlength |                |             입력 필드에 대한 최대 문자 수 정의              |
|    min    |                |                입력 필드에 대한 최소값 정의                 |
|  pattern  |                |               입력 값을 확인할 정규 식을 지정               |
| readonly  |                |       입력 필드를 읽기 전용으로 지정(변경할 수 없음)        |
| required  |                |                    필수 입력 필드를 지정                    |
|   size    |                |             입력 필드의 너비(문자 단위)를 지정              |
|   step    |                |          입력 필드에 대한 규칙적인 번호 간격 지정           |
|   value   |                |                  입력 필드의 기본값을 지정                  |







