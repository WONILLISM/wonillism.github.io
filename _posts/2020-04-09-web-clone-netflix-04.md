---
title: "[WEB] Netflix 따라 만들기 04. Javascript 구조"
excerpt: "Netflix 따라 만들기"

categories:
    - WEB
tags:
    - 넷플릭스
    - Netflix
    - coding test
    - front end
    - 프론트 엔드
    - vanilla javascript
    - 자바스크립트
    - tmdb
    - the movie database
    - html
    - css
    - clone
use_math: true;

last_modified_at: 2020-04-09  
---

{% include GoogleAdSenseSidebar.html %}  

학부시절 많은 프로젝트를 하면서 팀원들이 **API** 호출을 하는 것을 많이 봤지만 직접 호출해본것은 이번이 처음이다. **javascript** 도 처음이고 **API** 도 처음이고... 프로젝트를 진행하면서 많은 어려움을 겪었지만, [u_story](https://uyoo-story.tistory.com/) 주인장과 다른 친구들의 도움을 통해 프로젝트를 완성할 수 있었다.  



## Javascript 구조   

[![](/assets/Web/clone_netflix/javascript_structure_img.png)](/assets/Web/clone_netflix/javascript_structure_img.png)

  

### header.js

**addEventListener()** 를이용하여 마우스 휠 이벤트가 발생할 때 헤더 부분의 배경색을 바꿔주었다.  

**addEventListener()** 는 지정한 이벤트가 대상에 전달될 때 마다 호출 할 함수를 설정한다. 일반적 대상은 **Element, Document, Window** 지만 **XMLHttpRequest** 와 같이 이벤트를 지원하는 모든 객체를 대상으로 지정할 수 있다.  

>target.addEventListener(type, listener[, options]);
>target.addEventListener(type, listener[, useCapture]);

+ type : 반응할 이벤트 유형을 나타냄
+ listener : 지정된 타입의 이벤트가 발생했을 때, 알림을 받는 객체이다. 
+ options : 이벤트 리스너에 대한 특성을 지정하는 옵션 객체이다.
+ useCapture : DOM 트리의 하단에 있는 **EventTarget** 으로 전송하기 전에, 등록된 **listener** 로 이 타입의 이벤트의 전송여부를 나타내는 **Boolean** 값이다.  

```js
const headerContainer = document.querySelector('.header_container');
function init() {
    window.addEventListener('scroll',
        function (e) {
            scroll_position = window.scrollY;
            if (scroll_position!=0) {
                //console.log("wheel down");
                headerContainer.style.background = 'black';
            }
            else {
                headerContainer.style.background = 'linear-gradient(to bottom, rgba(0, 0, 0, 0.7) 10%, rgba(0, 0, 0, 0))';
            }
        }
    );
}
```



addEventListener를 이용하여 `scroll` 이벤트를 받고 그 스크롤 Y값을 이용하여 움직임 여부를 체크하여 움직였으면 배경값에 **검정색** 을 주고, 상단이라면 **linear-gradient** 를 이용하여 그라데이션을 주었다.  

### index.js  

여기서 처음 접했던 javascript는 두 가지이다. **async, await** 와 **map** .

+ **async function** 선언은 **AsyncFunction** 객체를 반환하는 하나의 비동기 함수를 정의한다.
  **async** 함수에는 **await** 식이 포함될 수 있는데, 이 식은 **async** 함수의 실행을 일시 중지하고 전달 된 **Promise** 의 해결을 기다린 다음 **async** 함수의 실행을 다시 시작하고 완료후 값을 반환한다.

솔직히 무슨말인지 아직 잘 모르겠다. 그냥 api요청을 완료할 때 까지 javascript에 작성된 함수들을 실행시키지 않는다. 정도로 이해하고있다. **promise** 라는 것도 있는데 음... 좀 더 공부해야할 것 같다.

+ **map** : map 객체는 요소의 삽입 순서대로 원소를 순회한다. 반복문은 각 순회에서 `[key, value]` 로 이루어진 배열을 반환한다.

알고리즘에 사용하는 **map** 과 동일한 것 같다.  

{% include GoogleAdSensePost.html %}    

  

별거 아니라면 아닐 수 있는 프로젝트지만 나에겐 뭔가 조금이나마 프론트엔드 개발을 했구나 싶은 프로젝트였다. 공부를 하면 할수록 알아가야할게 태산이다...  

해당 코드를 일일이 다 분석할 수 없어 중요한 부분과 처음 접했던 부분만 정리했다.  
전체 코드는 github로 가면 볼 수 있다.  
[WONILLISM github](https://github.com/WONILLISM/Development-FrontEnd/tree/master/ImitateNetflix/WONILLISM)  


