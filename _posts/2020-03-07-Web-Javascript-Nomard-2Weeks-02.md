---
title: "[Javascript] vanillaJS 2주완성 02"
excerpt: "vanillia JS로 크롬 앱 만들기"

categories:
    - WEB
tags:
    - javascript
    - 자바스크립트
    - vanilla JS
    - vanilla
    - 웹 개발
    - 프론트 엔드
    - front end
use_math: true;
last_modified_at: 2020-03-07  
---  

> __HTML/CSS__ 공부  
> 개발 언어 : __javascript__  
> 개발 환경 : __Visual studio Code__  
> 강의 : [Vanillia JS 2주 완성반 with Nomard](https://academy.nomadcoders.co/courses/enrolled/435558)  

  

## JS DOM functions

### BOM 이란?

__BOM(Browser Object Model)__ 

브라우저와 관련된 객체들의 집합으로서 __BOM__을 이용하여 Browser와 관련된 기능들을 구성한다. 이 __BOM__을 이용해서 Browser와 관련된 기능들을 구성한다.   

__BOM__의 최상위 객체는 window라는 객체이다.

### DOM 이란?  
__DOM(Document Object Model)__은 __window__ 객체의 하위 객체이기도 하다.  

넓은 의미로 웹 브라우저가 __HTML__ 페이지를 인식하는 방법을 의미하고 조금 좁은 의미로 보면 __document__ 객체와 관련된 객체의 집합을 의미한다.  

즉, html의 __태그__나 __클래스__, __아이디 __를 __Javascript__가 이용할 수 있는 객체로 만들어 주는 역할을 한다.  

__DOM 구조__  

[![](/assets/Web/Javascript/2020-03-07-Web-Javascript-Nomard-02-img01.png)](/assets/Web/Javascript/2020-03-07-Web-Javascript-Nomard-02-img01.png)  

### DOM을 사용하는 방법

`html 파일`

```html
<body>
    <h1 id = "title">This works!</h1>
    <script src="src/index.js"></script>
</body>
```



`js 파일`

```js
const title = document.getElementById("title");

title.innerHTML = "Fuck!";
```

[![img02](/assets/Web/Javascript/2020-03-07-Web-Javascript-Nomard-02-img02.png)](/assets/Web/Javascript/2020-03-07-Web-Javascript-Nomard-02-img02.png)



`console.dir(title)`을 이용하여 `title`의 하위객체들을 살펴보자.  

[![image03](/assets/Web/Javascript/2020-03-07-Web-Javascript-Nomard-02-img03.png)](/assets/Web/Javascript/2020-03-07-Web-Javascript-Nomard-02-img03.png)  

위와 같은 방식으로 무수히 많은 객체들의 상태를 확인할 수 있다.  

  

### getElementBy... VS querySelector  

> [참고1](https://humahumahuma.tistory.com/122)
> [참고2](https://whatabouthtml.com/difference-between-getelementbyid-and-queryselector-180)

둘 다 __DOM__에서 제어할 수 있으나 __querySelector__는 첫번째 자식을 반환한다.  

|                        getElementby..                        |                        querySelector                         |
| :----------------------------------------------------------: | :----------------------------------------------------------: |
|     예) document.getElementById('**web-id**').innerHTML;     |     예) document.querySelector('**#web-id**').innerHTML;     |
| 만약에 해당 선택자에 맞는 element가 없다면 null을 반환한다.  | 해당 선택자에 맞는 element 뭉탱이 중에서 첫번째 놈을 반환한다.querySelectorAll는 모든 element뭉탱이(= node list)를 반환한다.[*** element와 node의 차이?** (클릭) ](https://ohgyun.com/333) 해당하는 것이 없다면 null을 반환한다. |
|                                                              | 인접한 태그들끼리의 상대적인 위치를 비교하여 가져오고 싶다면 querySelector를 써야한다.<br/><br/>예1) document.querySelector('ul li.web-class').innerHTML;<br/><br/>예2) document.querySelector('li.web-class').innerHTML; |
|             처리속도는 getElementBy..가 빠르다.              |                                                              |
| 리턴값은 HTMLCollection (name, id, index number로 HTMLCollection의 항목(itmes)들에 접근할 수 있다) | 리턴값은 NodeList (index Number로만 NodeList의 항목(items)들에 접근할 수 있다) |

  

