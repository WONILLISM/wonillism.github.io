---
title: "[Algorithm] Backtracking(백트래킹)"
excerpt: "Backtracking 알고리즘을 알아보자"

categories:
    - Algorithm
tags:
    - backtracking
    - 백트래킹
    - 완전탐색
    - 알고리즘
    - algorhtim
    - BOJ
    - DFS
    - c++
    - cpp  
    - boj
    - '15649'
    - N과 M '(1)'
use_math: true;

last_modified_at: 2020-04-02
--- 

백트래킹, 있는 그대로를 해석해보면 역추적? 정도 일까.. 그럼 어떻게?? 무슨 뜻이지? 라는 의문을 항상 가지고 있었다.  어떤 설명을 보면 **DFS** 와 무슨차이인가 싶기도하고.. 정확히 머리속에 정리가 안됐었다. 이번 포스팅에서 그 의문을 풀어보고자한다.  

{% include GoogleAdSenseSidebar.html %}  


# Backtracking(백트래킹)

**퇴각검색** (백트래킹) 은 한정 조건을 가진 문제를 풀려는 전략이다. 

문제가 한정 조건을 가진 경우 원소의 순서는 해결 방법과 무관하다. 이런 문제는 변수 집합으로 이루어지는데, 한정 조건을 구성하려면 각각의 변수들은 값이 있어야 한다. **퇴각검색** 은 모든 조합을 시도해서 문제의 해를 찾는다. 이 방식으로 많은 부분 조합들을 배제하여 풀이 시간을 단축시킨다. 

([출처: 위키백과]([https://ko.wikipedia.org/wiki/%ED%87%B4%EA%B0%81%EA%B2%80%EC%83%89](https://ko.wikipedia.org/wiki/퇴각검색)))  

결국 **완전탐색(Brute Force Search)** 를 해야한다는 소리다. 모든 경우를 탐색할 때 굳이 찾지 않아도 되는 조건을 탐색할 때 비효율적인 부분이 발생할 수 있다. 그래서 이와 같은 비효율적인 경로를 차단하고 조건에 맞는 루트를 탐색하는 방법이 **Backtriacking algorithm** 이다.  

말로만 설명해서는 이해하기가 좀 힘들것 같다. 그래서 후에 포스팅하려고했지만 백준 단계별로 풀기 백트래킹에 있는 첫번째 문제를 예시로 들겠다.

## [N과 M (1)](https://www.acmicpc.net/problem/15649)  

### 문제설명 

자연수 N과 M이 주어졌을 때 1부터 N까지 자연수 중 중복 없이 M개를 고른 수열을 출력하라.  

여기서 **가지치기(비효율적 탐색 버리기)** 를 해야할 부분은 중복된 경우를 이야기한다. 

예를들어 **N = 3, M = 2** 라고 주어지면 우선 모든 경우, 즉 공집합을 제외한 모든 부분집합은

{1}, {2}, {3}

{1,2}, {1,3}, {2,1}, {2,3}, {3,1}, {3,2}

{1,2,3}, {1,3,2}, {2,1,3}, {2,3,1}, {3,1,2}, {3,2,1}  

$_3P_1 + _3P_2 + _3P_3 = 15$  의 모든 경우 중에서 **순서는 허락하며 중복을 허락하지 않는** 경우는 

{1,2}, {1,3}, {2,1}, {2,3}, {3,1}, {3,2} 즉, $_3P_2$ 를 구하는 문제다.

재귀함수를 이용하여 **DFS** 와 **백트래킹** 을 이용해 문제를 해결하였다.  

여기서 가지치기에 해당하는 부분은  아래 두가지가 되겠다.

해당 노드에 방문을 했는지 체크하는 `visit` 배열로 중복 선택을 가지치기 하고 몇 개가 선택되었는지 확인하는 `cnt`를 이용하여 3개 의 탐색을 가지치기하여 `cnt==2`가 되었을 때 문제를 해결해 준다.

```cpp
if (cnt == m)
if (!visit[i])
```

![img01](/assets/Algorithm/2020-04-03-algorithm-backtracking-img01.png)
```cpp
#include<cstdio>
#include<iostream>
#include<vector>
#include<string>
#include<queue>
#include<deque>
#include<algorithm>
#define endl '\n';
#define ll long long
#define PII pair<int,int>
using namespace std;

const int MAX = 9;
vector<int> v;	//stack
bool visit[MAX];
int n, m;
void process(int cnt) {
	if (cnt == m) {
		for (int i = 0; i < v.size(); i++)
			cout << v[i] << " "; 
		cout << endl;
		return;
	}
	for (int i = 1; i <= n; i++) {
		if (!visit[i]) {
			visit[i] = true;
			v.push_back(i);
			process(cnt + 1);
			visit[i] = false;
			v.pop_back();
		}
	}
}
void solution() {
	process(0);
}
int main() {
	ios::sync_with_stdio(false);
	cin.tie(NULL);

	cin >> n >> m;
	solution();
	return 0;
}
```



{% include GoogleAdSenseSidebar.html %}  