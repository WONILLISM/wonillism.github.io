---
title: "[프로그래머스]디스크 컨트롤러"
excerpt: "프로그래머스 코딩테스트 연습"

categories:
    - Programmers
tags:
    - 프로그래머스
    - Programmers
    - 코딩테스트연습
    - 디스크컨트롤러
    - 알고리즘
    - 코딩
    - 코딩테스트
use_math: true
last_modified_at: 2019-12-01
---    
# [(lv3) 디스크 컨트롤러](https://programmers.co.kr/learn/courses/30/lessons/42627)   

## 문제
[![](/assets/Programmers/2019-12-01-Programmers-disk-controler-img01.jpg)](/assets/Programmers/2019-12-01-Programmers-disk-controler-img01.jpg)  
[![](/assets/Programmers/2019-12-01-Programmers-disk-controler-img02.jpg)](/assets/Programmers/2019-12-01-Programmers-disk-controler-img02.jpg)   
[![](/assets/Programmers/2019-12-01-Programmers-disk-controler-img03.jpg)](/assets/Programmers/2019-12-01-Programmers-disk-controler-img03.jpg)  
[![](/assets/Programmers/2019-12-01-Programmers-disk-controler-img04.jpg)](/assets/Programmers/2019-12-01-Programmers-disk-controler-img04.jpg)  
  
원리 자체는 알고있는 문제였지만 구현하기에는 어려운 문제였다. 평소 `디스크 스케쥴링` 문제를 풀어보면 어려움을 많이 겪었다.  
정보처리기사 필기를 준비하며 공부했던 기억을 떠올리며 알고리즘을 풀었다.  

## 문제 풀이  
우선 떠올랐던 스케쥴링 알고리즘은  
`FCFS(First Come First Served): 먼저 들어온 요청을 순서대로 처리하는 방식`과 `SJF(Shortest Job First): 평균 대기시간을 최소화하는 방식` 두 가지가 떠올랐다.  
문제를 해결하기 위해서는 `SJF`방식을 이용해야한다.  
1. 우선 주어진 `jobs`를 두 `int`형 요청시간과 작업시간을 순서로 가지는 `vector<Time> disks`에 복사한다.  
```cpp  
bool compare(Time a, Time b) {
	if (a.proc == b.proc)
		return a.req < b.req;
	else return a.proc < b.proc;
}
```
2. 위와 같은 비교함수를 이용하여 정렬하는데 설명을 하자면  
    + 처리시간이 짧은 순서로 정렬한다
    + 처리시간이 같으면 요청시간이 빠른 순서로 정렬한다
3. `disks`에 정렬된 정보들 중 요청시간이 빠른 작업을 찾기 위해 `if(cur.req<=t)`를 만족하는 요청시간을 찾고 없다면 `t(디스크 작동시간)`일 1초 늘려준다.  
리뷰하면서 느꼈는데 이 부분에 대해서 처리중인 작업이 없다면 바로 다음 작업을 가지고와서 처리하면 프로그램 시간을 줄일 수 있을 것 같다.  
4. `if(cur.req<=t)`를 만족하는 요청시간이 있다면 `t`에 `cur.proc`(현재 작업시간) 을 누적시켜준다.
5. `answer`에 대기시간과 작업시간을 더 한 값을 누적시켜주고 해당 요청을 `disks`에서 삭제하고 반복문을 종료한다.  
6. 위 3~5의 과정을 `disks`가 빌 때까지 반복한다.
7. `answer/jobs.size()`를 출력한다.  

```cpp
#include<iostream>
#include <vector>
#include <algorithm>
using namespace std;
int ans;
typedef struct Time {int req, proc;};
bool compare(Time a, Time b) {
	if (a.proc == b.proc)
		return a.req < b.req;
	else return a.proc < b.proc;
}
int solution(vector<vector<int>> jobs) {
	int answer = 0;
	vector<Time> disks;
	for (int i = 0; i < jobs.size(); i++) 
		disks.push_back({ jobs[i][0], jobs[i][1] });
	sort(disks.begin(), disks.end(), compare);
	int t = 0;
	while (!disks.empty()) {
		for (int i = 0; i < disks.size(); i++) {
			Time cur = disks[i];
			if (cur.req <= t) {
				t += cur.proc;
				answer += t - cur.req;
				disks.erase(disks.begin() + i);
				break;
			}
			if (i == disks.size() - 1)t++;
		}
	}
	answer /= jobs.size();
	return answer;
}
```  

