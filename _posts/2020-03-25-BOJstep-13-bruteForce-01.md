---
title: "[BOJ step 13] Brute Force 01. 블랙잭"
excerpt: "백준 단계별로 풀기 Brute Force 1번"

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
    - '2798'
    - 블랙잭
    - c++
    - cpp  
use_math: true;

last_modified_at: 2020-03-25  
---

백준 단계별로 풀기가 계속해서 업데이트 해서 단계가 뒤죽박죽이다... **2020-03-25** 기준 **Brute Force** 는 단계 13이다.  

솔직히.. 블로그 포스팅 한 것들 카테고리도 그렇고 태그도 그렇고 계속 업데이트하다보니 한다고 했지만 분류가 잘 안된게 많은 것 같다. 나중에 시간나면 정리좀 해야겠다.  




{% include GoogleAdSenseSidebar.html %}



## [블랙잭](https://www.acmicpc.net/problem/2798)

### 문제 설명

카드의 갯수 **N** ($3 \le N \le 100$) 이 주어지고 **N** 개 중 3장의 카드를 선택하여 합이 **M** ($10 \le M \le 30000$)이 넘지 않는 최댓값을 구하는 문제.   

앞서 포스팅한 일곱 난쟁이와 비슷한 문제다. 차이는 선택된 카드들의 합이 특정 숫자인지를 찾는 것이 아닌 특정 숫자(M) 보다 작으면서 최댓값을 찾는 문제다.  

### 문제 풀이

예전에 풀었던 소스 코드를 확인해보자.

이번 문제는 일곱 난쟁이와 달리 3개를 선택해야 하므로 **DFS** 를 **재귀함수** 로 구현하고 조합($_NC_3$ )을 이용하여 문제를 풀었다.  

**조합 구현 방식**  

[![](/assets/BOJ-step/2020-03-25-BOJ-Step13-01-img01.PNG)](/assets/BOJ-step/2020-03-25-BOJ-Step13-01-img01.PNG)

1. 위 그림과 같이 i를 기준으로 j를 늘려가며 다음 인덱스에 방문하며 선택했다고 표시 해준다
2. 선택한 카드의 갯수가 3이면, 세 장의 카드의 합이 sum 보다 작으면 최댓값 계산을 해준다
3. 그렇지 않다면 위 그림처럼 i와 j를 반복한다.   

소스 코드

```cpp
#include<cstdio>
const int MAX_N = 101;
int n, m, ans;
// int num[MAX_N];
bool visit[MAX_N];
void process(int j, int cnt, int sum) {
	if (cnt == 3) {
		if (sum <= m) {
			if (ans < sum)ans = sum;
		}
		return;
	}
	for (int i = j; i < n; i++) {
		if (!visit[i]) {
			visit[i] = true;
			process(i, cnt + 1, sum + num[i]);
			visit[i] = false;
		}
	}
}
void solution_2798() {
	scanf("%d%d", &n, &m);
	for (int i = 0; i < n; i++)
		scanf("%d", &num[i]);
	process(0, 0, 0);
	printf("%d", ans);
}
int main() {
	solution_2798();
	return 0;
}
```







{% include GoogleAdSenseSidebar.html %}
