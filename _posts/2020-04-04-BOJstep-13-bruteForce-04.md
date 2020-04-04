---
title: "[BOJ step 13] Brute Force 04. 체스판 다시 칠하기"
excerpt: "백준 단계별로 풀기 Brute Force 4번"

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
    - '1018'
    - 체스판 다시 칠하기
    - c++
    - cpp  
use_math: true;

last_modified_at: 2020-04-04  
---

{% include GoogleAdSenseSidebar.html %}

# [체스판 다시 칠하기](https://www.acmicpc.net/problem/1018)

### 문제 설명

흰색 또는 검정색으로 칠해진 $M \times N$ 체스판이 있는데 $8 \times 8$ 만큼으로 잘라 체스판을 검정색과 흰색이 번갈아가도록 만들기 위해 다시 칠해지는 색의 수 중 최솟값을 구하는 문제이다.  



### 문제 풀이

**N** 과 **M** 의 범위가 크지 않으므로 모든 칸에 대하여 $8 \times 8$ 칸 만큼씩 탐색하는 **완전탐색** 문제다.  

$8 \le N,M \le 50$ 이므로 $O(N \times M \times 8 \times 8) = 16000$  밖에 안된다.  

1. $8 \times 8$ 짜리 흰색이 먼저 칠해진 판과 검정색이 먼저 칠해진 판을 미리 만들어 놓는다.  
2. `process(i,j)` 모든 칸에 대하여 탐색을 하고 그 칸을 시작으로 미리 칠해둔 판과 비교하여 다를 경우 `cntW, cntB`를 각각 세어주어 최솟값을 구하는 과정을 반복한다.  




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

const int MAX = 51;
char board[MAX][MAX];
int visit[MAX][MAX];
int N, M, sx, sy, ans = 32;

int dx[] = { 1,0 }, dy[] = { 0,1 };

string white[8] = {
		{ "WBWBWBWB" },
		{ "BWBWBWBW" },
		{ "WBWBWBWB" },
		{ "BWBWBWBW" },
		{ "WBWBWBWB" },
		{ "BWBWBWBW" },
		{ "WBWBWBWB" },
		{ "BWBWBWBW" }
};
string black[8] = {
		{ "BWBWBWBW" },
		{ "WBWBWBWB" },
		{ "BWBWBWBW" },
		{ "WBWBWBWB" },
		{ "BWBWBWBW" },
		{ "WBWBWBWB" },
		{ "BWBWBWBW" },
		{ "WBWBWBWB" }
};
void process(int y, int x) {
	int cntW = 0, cntB = 0;
	for (int i = 0; i < 8; i++) {
		for (int j = 0; j < 8; j++) {
			if (white[i][j] != board[y + i][x + j])cntW++;
			if (black[i][j] != board[y + i][x + j])cntB++;
		}
	}
	ans = min(ans, min(cntW,cntB));
}
void solution() {
	for (int i = 0; i < N - 7; i++) {
		for (int j = 0; j < M - 7; j++) {
			process(i, j);
		}
	}
	cout << ans << endl;
}
int main() {
	ios::sync_with_stdio(false);
	cin.tie(NULL);

	cin >> N >> M;
	for (int i = 0; i < N; i++)
		cin >> board[i];
	solution();
	return 0;
}
```



{% include GoogleAdSenseSidebar.html %}
