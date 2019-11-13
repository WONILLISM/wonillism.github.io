---
title: "[프로그래머스]2 x n 타일링"
excerpt: "dp를 활용한 2xn 타일링"

categories:
    - Programmers
tags:
    - 프로그래머스
    - Programmers
    - 코딩테스트연습
    - 2xn타일링
    - DP
    - 동적프로그래밍
    - memoization
    - 메모이제이션
last_modified_at: 2019-11-12
---  
프로그래머스 문제도 정복해보자. 프로그래머스 코딩테스트연습에 있는 문제들 중 lv3~lv5까지의 문제만 쭈욱 풀어보기로 했다.  
평소 백준이나 삼성 기출 문제 형식에 익숙해져있어서 프로그래머스 문제는 같은 문제라도 좀 느낌이 달랐다. 아직까지도 `STL`사용에 익숙하지 않아서 그런 것 같다. 프로그래머스 문제들은 main함수, 예시 입력 부분은 건드릴 필요 없이 문제에 대한 논리적 풀이 과정만을 작성하면된다. 크게 다를 것은 없지만... 뭔가 더 어렵다.. 익숙해져 보자.  
  
한 달 전부터 시작했는데 좀 바빠서 미뤄뒀더니 문제가 너무 많이 쌓여버렸다... 미루지말자 ㅠㅜ  
  
# [(lv3) 2 x n 타일링](https://programmers.co.kr/learn/courses/30/lessons/12900)   

  
## 문제
예전에 `DP(다이나믹프로그래밍`를 살짝 공부하면서 풀어봤던 문제이다. 이 문제를 통해서 `memoization`이 뭔지 알게됐다. 나중에 `DP(다이나믹프로그래밍`에 대해 포스팅을 해야겠다.  

[![](/assets/Programmers/2019-11-12-Programmers-2xn타일링-img01.png)](/assets/Programmers/2019-11-12-Programmers-2xn타일링-img01.png)  
  
## 문제 풀이

  
