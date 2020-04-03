---
title: "[프로그래머스]단어 변환"
excerpt: "프로그래머스 코딩테스트 연습"

categories:
    - Programmers
tags:
    - 프로그래머스
    - Programmers
    - 코딩테스트연습
    - 단어 변환
    - 알고리즘
    - 코딩
    - 코딩테스트
use_math: true
last_modified_at: 2019-12-01
published : false
---    
# [(lv3) 단어 변환](https://programmers.co.kr/learn/courses/30/lessons/43163)   

## 문제
[![](/assets/Programmers/2019-12-01-Programmers-word-change-img01.jpg)](/assets/Programmers/2019-12-01-Programmers-word-change-img01.jpg)   
`BFS/DFS`문제다. 문제를 처음 접했을 때는 이게 왜 `BFS/DFS`문제인지 좀 와닿지 않았었는데 포스팅을 하면서 다시 복기하니깐 엄청 간단한 문제구나 싶었다. 이 문제는 `DFS`로 풀었는데 평소 `DFS`를 이용할 때 `재귀함수`를 이용했는데 이번에는 `stack`을 이용하여 `반복문`으로 풀어봤다.  

## 문제 풀이  
1. 각 단어 `words`가 시작 노드가 아니므로 각 단어들이 변환 가능한 단어인지 하나씩 확인 한다.
2. 만약 변환가능한 단어라면 `DFS`할 준비를한다. 방문 체크를 위한 해당 단어들의 인덱스를 기준으로 `visit`을 만들고 변환 가능한 단어의 인덱스에 방문체크를하고 `DFS`를 위한 스택에 푸시한다.  
3. 그래프에서 연결된 노드 대신 `cur`의 단어가 변환 가능한 단어 인지 찾고 스택에 푸시한다. 방문 체크는 이동한 `step`을 누적하여 저장한다.  
4. `cur`의 단어가 `target`단어라면 `visit`에 저장된 `cur`의 `step`을 리턴하여 출력한다. 
5. 4번과정을 찾을 때 까지 반복한다.  
  
아래는 `stack`을 이용한 `DFS`와 `queue`를 이용한 `BFS`를 이용한 풀이 두 가지로 풀어봤다.  
큐를 이용한 풀이는 방문체크에 누적하지 않고 큐에 step을 푸시한다.  

```cpp
#include <string>
#include <vector>
#include<queue>
using namespace std;

bool chkString(string a, string b) {
	int cnt = 0;
	for (int j = 0; j < b.size(); j++) {
		if (a[j] != b[j])cnt++;
	}
	return cnt == 1 ? true : false;
}
int solution(string begin, string target, vector<string> words) {
	int answer = 0;
	int n = words.size();
	for (int i = 0; i < n; i++) {
		if (chkString(begin, words[i])) {
			vector<int> visit(n, 0);
			vector<pair<string, int>> v;
			string cur = words[i];
			int curIdx = i;
			visit[i] = 1;
			v.push_back({ cur,curIdx });
			while (!v.empty()) {
				cur = v.back().first, curIdx = v.back().second;
				v.pop_back();
				if (cur == target)return visit[curIdx];
				for (int next = 0; next < words.size(); next++) {
					if (!visit[next] && chkString(cur, words[next])) {
						visit[next] = visit[curIdx] + 1;
						v.push_back({ words[next], next});
					}
				}
			}
		}
	}
	return answer;
}
```  
```cpp
#include <string>
#include <vector>
#include<queue>
using namespace std;

vector<string> W;
typedef struct info {
	string s;
	int step;
};
queue<info> q;
int Visit[50];
string S, E;
void isChange(string s, int step) {
	for (int i = 0; i < W.size(); i++) {
		int cnt = 0;
		if (!Visit[i]) {
			for (int j = 0; j < W[i].size(); j++) {
				if (W[i][j] != s[j])cnt++;
			}
			if (cnt == 1) {
				Visit[i] = true;
				q.push({ W[i], step + 1 });
			}
		}
	}
}
int process() {
	info cur = { S,0 };
	isChange(cur.s, cur.step);

	while (!q.empty()) {
		cur = q.front();
		q.pop();
		if (cur.s == E)return cur.step;
		if (cur.step >= W.size())return 0;
		isChange(cur.s, cur.step);
	}
	return 0;
}
int solution(string begin, string target, vector<string> words) {
	int answer = 0;
	W = words;
	S = begin;
	E = target;
	answer = process();
	return answer;
}
``` 

