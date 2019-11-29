---
title: "[프로그래머스]네트워크"
excerpt: "프로그래머스 코딩테스트 연습"

categories:
    - Programmers
tags:
    - 프로그래머스
    - Programmers
    - 코딩테스트연습
    - 네트워크
use_math: true
last_modified_at: 2019-11-29
---    
# [(lv3) 네트워크](https://programmers.co.kr/learn/courses/30/lessons/43162)   

## 문제
[![](/assets/Programmers/2019-11-29-Programmers-network-img01.jpg)](/assets/Programmers/2019-11-29-Programmers-network-img01.jpg)  
[![](/assets/Programmers/2019-11-29-Programmers-network-img02.jpg)](/assets/Programmers/2019-11-29-Programmers-network-img02.jpg)  
[![](/assets/Programmers/2019-11-29-Programmers-network-img03.jpg)](/assets/Programmers/2019-11-29-Programmers-network-img03.jpg)  
간단한 `BFS`문제이다. 주어지는 그래프가 하나의 정점도 자기 자신으로 돌아가는 그래프라고 생각하고 이어진 그래프가 몇 개의 덩어리로 나뉘는지?를 세어주면 되는 문제이다.  

  
## 문제 풀이  
1. 주어지는 그래프의 정점들은 모두다 자기자신과 연결되어 있으므로 `n x n`의 그래프라면 `n`개의 정점에 대해 모두 탐색해주면 된다.  
2. 각 정점들을 `k`라 할 때 해당 정점에 방문한적이 없으면 `visit`에 방문체크를 하고`큐`에 현재 좌표를 넣어주고 `BFS` 탐색을 시작한다. 이 때 모든 정점은 자기자신과 이어져있으므로 해당 정점에서 시작할때 덩어리의 시작이라고 생각하고 카운트(`answer++`)해 준다.
3. 현재 큐의 `front`에 있는 정점을 `cur`(현재 정점)이라고하고 현재 정점과 이어진 다음 정점들을 찾기위해 `0~n`까지 정점을 `next`라 하고 이어져 있으면(`computer[cur][next]=1`) 큐에 `push`해주고 방문체크를 해준다.  
4. 위 과정을 큐가 빌때까지 반복해주고 큐가 빈다면 다음 정점에 대해 `BFS`를 해준다.

__주의해야할 점__  
정말 바보같은 실수로 시간을 보냈었다. 나름 `bfs`를 잘 알고 있다고 생각해서 다음 정점에 대해 탐색할 때 범위를 (cur ~ n) 즉 현재 이전의 정점들은 이미 탐색해왔으니 생각할 필요가 없다고 생각했다. 하지만 항상 그래프의 정점들은 다음 정점이 현재 정점보다 크지않다.  
예를들어 __(1 - 2 - 3)__ 이라면 위와 같이 범위를 지정해도 상관이 없겠지만 __(1 - 3 - 2)__ 이와 같이 되어 있을경우에는 현재정점이 3일 때 __(3-2)__ 를 탐색하지 못한다.  
  
`STL`을 잘 사용하지 않았을때는 배열을 이용하여 간단하게 큐를 구현하여 문제를 풀곤했다. 두 방법 모두 익숙해지기 위해서 `STL`을 사용한 방법과 사용하지 않은 방법으로 문제를 풀어봤다.
```cpp
#include<iostream>
#include<vector>
#include<queue>
using namespace std;
int solution(int n, vector<vector<int>> computers) {
	int answer = 0;
	queue<int> Q;
	vector<int> visit(n, 0);
	for (int k = 0; k < n; k++) {
		int cur = k;
		if (!visit[cur]) {
			Q.push(cur);
			visit[cur] = 1;
			answer++;
			while (!Q.empty()) {
				cur = Q.front();
				Q.pop();
				for (int i = 0; i < n; i++) {
					int next = i;
					if (!visit[next] && computers[cur][next]) {
						Q.push(next);
						visit[next] = 1;
					}
				}
			}
		}
	}
	return answer;
}
```  
```cpp
#include<iostream>
#include <string>
#include <vector>

using namespace std;
int Q[200 * 200], f, r, cnt;
int visit[200];
void bfs(int n, vector<vector<int>> &map) {
	for (int k = 0; k < n; k++) {
		if (!visit[k]) {
			++cnt;
			int cur = k;
			Q[r++] = cur;
			visit[cur] = 1;
			while (f != r) {
				cur = Q[f++];
				for (int i = cur; i < n; i++) {
					if (map[i][cur] && !visit[i]) {
						visit[i] = 1;
						Q[r++] = i;
					}
				}
			}
		}
	}
}
int solution(int n, vector<vector<int>> computers) {
	int answer = 0;
	bfs(n, computers);
	return answer = cnt;
}  
```
