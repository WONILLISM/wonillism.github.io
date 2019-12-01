---
title: "[프로그래머스]가장 먼 노드"
excerpt: "프로그래머스 코딩테스트 연습"

categories:
    - Programmers
tags:
    - 프로그래머스
    - Programmers
    - 코딩테스트연습
    - 가장 먼 노드
    - 알고리즘
    - 코딩
    - 코딩테스트
use_math: true
last_modified_at: 2019-12-01
---    
# [(lv3) 가장 먼 노드](https://programmers.co.kr/learn/courses/30/lessons/49189)   
간단한 `BFS`문제다.  
1번 노드부터 가장 멀리 떨어져있는 노드, 즉 터미널 노드의 개수를 찾아주면 되는 문제이다.  
`BFS`나 `DFS` 어떤 탐색법으로든지 풀 수 있을 것 같다.
## 문제
[![](/assets/Programmers/2019-12-01-Programmers-furthest-node-img01.jpg)](/assets/Programmers/2019-12-01-Programmers-furthest-node-img01.jpg)  

## 문제 풀이  
1. 1번 노드 방문체크하고 큐에 넣는다.
2. 현재 노드와 이어진 다음 노드를 찾고 방문하지 않았으면 큐에 푸시 한다.  이 때 방문체크를 `step`(움직인 거리)와 같이 생각한다. `visit[next] = visit[cur] + 1`의 방법으로 움직인 거리를 계산 해준다.
3. 터미널 노드의 개수를 세어주기 위해 `visit[next]`의 최대값을 찾아준다.  
4. 위 과정을 큐가 빌 때까지 반복해준다.
5. 터미널 노드를 세어주기 위해 `visit[i]==Max`인 경우를 카운트하여 답을 출력한다.  
  
아래는 인접 리스트을 이용한 방법과 인접 행렬을 이용한 방법 모두 구현해보았다.  

```cpp
#include <vector>
#include<queue>
using namespace std;

int solution(int n, vector<vector<int>> edge) {
	int answer = 0, Max = 0;
	queue<int> q;
	vector<int> visit(n + 1, 0);
	vector<vector<int>> g(n + 1, vector<int>());
	for (int i = 0; i < edge.size(); i++) {
		int u = edge[i][0], v = edge[i][1];
		g[u].push_back(v);
		g[v].push_back(u);
	}
	visit[1] = 1;
	q.push(1);
	while (!q.empty()) {
		int cur = q.front();
		q.pop();
		for (int i = 0; i < g[cur].size(); i++) {
			int next = g[cur][i];
			if (!visit[next] && next != 0) {
				visit[next] = visit[cur] + 1;
				q.push(next);
				if (visit[next] > Max)Max = visit[next];
			}
		}
	}
	for (int i = 1; i <= n; i++)
		if (Max == visit[i])answer++;
	return answer;
}
```  
```cpp  
int Visit[20001], ans, Max;
int Mat[20001][20001];
queue<int> q;
void process(int n){
	int cur = 1;
	Visit[cur] = 1;
	q.push(cur);
	while (!q.empty()) {
		cur = q.front();
		q.pop();
		for (int i = 1; i <= n; i++) {
			if (Mat[cur][i] && !Visit[i]) {
				Visit[i] = Visit[cur] + 1;
				q.push(i);
				if (Max < Visit[i])Max = Visit[i];
			}
		}
	}
}
int solution(int n, vector<vector<int>> edge) {
	int answer = 0;
	for (int i = 0; i < edge.size(); i++)
		Mat[edge[i][0]][edge[i][1]] = Mat[edge[i][1]][edge[i][0]] = 1;
	process(n);
	for (int i = 1; i <= n; i++)
		if (Max == Visit[i])ans++;
	answer = ans;
	return answer;
}
```

