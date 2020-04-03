---
title: "[BOJ step 13] Brute Force 02. 분해합"
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
    - '2231'
    - 분해 합
    - c++
    - cpp  
use_math: true;

last_modified_at: 2020-03-27  
published : false
---



요즘 난이도가 낮은 문제드를 풀며, 혹은 코딩테스트를 보면서 많이 느끼는데 간단한 문제들을 오히려 너무 어렵게 생각해서 문제를 복잡하게 풀다가 시간을 너무 많이 날리는 것 같다. 
알고리즘은... 너무 어렵다 ... 아직도 부족한 것 같다.

{% include GoogleAdSenseSidebar.html %}

# [분해합](https://www.acmicpc.net/problem/2231)


### 문제 설명

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
