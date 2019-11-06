---
title: "[c++]sort()"
excerpt: "c++ STL의 sort() 함수를 알아보자"

categories:
    - C++_STL
tags:
    - C++
    - STL
    - 표준라이브러리
    - 알고리즘
    - 정렬
    - sort
    - 자료구조
last_modified_at: 2019-11-06
---  
자료구조에는 여러가지 정렬 방법이 있다. 그 정렬 방법에따라 시간 복잡도는 `O(n^2)`, `O(nlogn)`등으로 나뉜다.  
[![](/assets/cppSTL/sort.gif)](/assets/cppSTL/sort.gif)
##### 출처 : <http://www.todayhumor.co.kr/board/view.php?table=bestofbest&no=200940>  
정렬에 대해 구글링을 하다가 우연히 발견한 gif이다. 모든 정렬들의 속도를 비교하며 한눈에 볼 수 있어서 매우 좋은 것 같다.  
<https://www.toptal.com/developers/sorting-algorithms> 여기서 직접 하나씩 실행 할 수 있다.  
  
많은 정렬 방법들이 있지만 알고리즘 문제를 풀 때 직접 작성하지 않고 c++ STL에 내장되어있는 sort()함수에 대해서 알아보자.  
  
