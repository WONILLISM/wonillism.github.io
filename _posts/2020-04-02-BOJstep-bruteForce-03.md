---
title: "[BOJ step 13] Brute Force 03. 덩치"
excerpt: "백준 단계별로 풀기 Brute Force 2번"

categories:
    - BOJ_Step
tags:
    - brute force
    - 브루트 포스
    - 완전탐색
    - 야만적인 힘
    - 알고리즘
    - algorhtim
    - BOJ
    - '7568'
    - 덩치
    - c++
    - cpp  
use_math: true;

last_modified_at: 2020-04-02  
---

{% include GoogleAdSenseSidebar.html %}

# [덩치](https://www.acmicpc.net/problem/7568)


### 문제 풀이

1. 각 덩치들의 `Rank`를 모두 1로 준다.
2. 한 덩치 `i`를 기준으로 잡고 나머지 덩치 `j`들을 모두 탐색한다. ( $_NC_2$의 모든 경우 )
3. 이 때 `i` 보다 `j`의 키와 몸무게가 모두 작으면 `Rank[j]++` 해준다.
4. 위 과정을 모든 덩치들에 대해 반복하여 `Rank` 벡터를 순서대로 출력해주면 된다.  

```cpp
#include <iostream>
#include <vector>
#include <queue>

#define PII pair<int,int>

using namespace std;

int N;
vector<PII> p;
vector<int> Rank;

void solution() {
	for (int i = 0; i < N; i++) {
		for (int j = 0; j < N; j++) {
			if (p[i].first < p[j].first && p[i].second < p[j].second) {
				Rank[i]++;
			}
		}
	}
	for (auto a : Rank)
		cout << a << " ";
	cout << endl;
}
int main() {
	ios::sync_with_stdio(false);
	cin.tie(NULL);

	cin >> N;
	for (int i = 0; i < N; i++) {
		int x, y;
		cin >> x >> y;
		p.push_back({ x,y });
		Rank.push_back(1);
	}
	solution();
	return 0;
}
```



{% include GoogleAdSenseSidebar.html %}
