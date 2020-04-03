---  
title: "[심심풀이/잡동사니] p5.js - 크롬 공룡 게임"
excerpt: "Clone chrome dino game"

categories:
    - odds and ends
tags:
    - 'p5.js'
    - processing
    - 프로세싱
    - game
    - 게임
    - 게임만들기
    - 크롬 공룡 게임
    - chrome
    - dino
    - game
use_math: true;

last_modified_at: 2020-03-31
published : false
---  

학부시절 배웠던 **processing** 이란 **IDE** 를 이용하여 게임을 만들었다. 중학생 코딩과외를 하면서 시작한 프로젝튼데 생각보다 어려웠는지 잘 따라오지 못해서 많이 아쉬웠다.  

{% include GoogleAdSenseSidebar.html %}

# Processing  

**프로세싱(Processing)** 은 컴퓨터 프로그래밍의 본질을 시각적 개념으로 프로그래머가 아닌 사람들에게 교육할 목적으로 뉴 미디어 아트, 시각 디자인 공동체를 위해 개발된 오픈 소스 프로그래밍 언어이자 통합개발환경(IDE)이다. 2001년 MIT 미디어 연구소에서 케이시 리아스와 벤자민 프라이가 시작했다.

> [출처: 위키백과](https://ko.wikipedia.org/wiki/%ED%94%84%EB%A1%9C%EC%84%B8%EC%8B%B1_(%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D_%EC%96%B8%EC%96%B4)) 

**Processing** 은 기본적으로 **JAVA** 가 기본언어지만 **Javascirpt** , **Python** 으로 만들 수 있는 라이브러리가 존재한다. 요즘 한창 **Javascript** 를 공부하고 있어서 **Javascript** 를 언어로 선택했다.  

**Processing IDE** 를 다운받아 **js** 라이브러리를 설치하여 사용해도되지만 **Javascript** 라이브러리를 기반으로한 **IDE** 를 웹에서도 제공한다.  

**[웹 IDE : p5.js](https://editor.p5js.org/)**   

  

## Example 

학부시절 내가 **Processing** 에 빠졌던 이유는 **Processing** 로 코딩해서 만들어진 **Art** 들을 보고 눈이 반짝반짝 해졌었다. 예술하는 사람들이 머리도 좋네... 라는 생각을 했었던 기억이난다.

![necessary-disorder tutorials](https://necessarydisorder.files.wordpress.com/2019/02/agif3opt.gif?w=356)
![Animation Processing GIF - Find & Share on GIPHY](https://media0.giphy.com/media/EMxPitL8r0fQY/source.gif)
![Coding GIF | Gfycat](https://thumbs.gfycat.com/CheerySeparateGoldeneye-size_restricted.gif)
![Pixel Art Cube GIF - Find & Share on GIPHY](https://media3.giphy.com/media/lkGfNhutRpcg8/source.gif)  

> [출처: 구글 이미지 검색](https://www.google.com/search?q=processing+animation&tbm=isch&ved=2ahUKEwiii4LStcToAhWnG6YKHVCDBJcQ2-cCegQIABAA&oq=processing+animation&gs_lcp=CgNpbWcQAzIECCMQJzIECCMQJzIECAAQEzIECAAQEzIICAAQBRAeEBMyCAgAEAUQHhATMggIABAFEB4QEzIICAAQBRAeEBMyCAgAEAgQHhATUKUNWLUQYMITaABwAHgAgAGuAYgBrgWSAQMwLjSYAQCgAQGqAQtnd3Mtd2l6LWltZw&sclient=img&ei=9Q-DXuK8Eae3mAXQhpK4CQ&bih=794&biw=1466&rlz=1C1OKWM_enKR884KR884#imgrc=c0sx_lJgtt-nCM&imgdii=yxMqLAyWScelbM)  

{% include GoogleAdSenseSidebar.html %}

**Processing(프로세싱)** 은 기본적으로 초기에 한번 호출하는 `void setup()` 함수와 **60frame(default)** 마다 반복해서 호출하는 `void draw()` 함수로 이루어져있는데 이를 이용해서 **animation** 을 만들 수 있다.  

저런 반복적인 성질을 이용하여 **chrome** 이스터 에그인 공룡게임을 만들어 보았다.  

[![dino game](/assets/odds_and_ends/Processing/clone_dino_game.png)](https://wonillism.github.io/odds-and-ends/chrome-dino-clone/)  

이미지를 클릭하면 직접 해볼수 있다.  



{% include GoogleAdSenseSidebar.html %}