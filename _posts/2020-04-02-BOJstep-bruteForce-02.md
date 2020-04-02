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

last_modified_at: 2020-04-02  
---

{% include GoogleAdSenseSidebar.html %}

# [분해합](https://www.acmicpc.net/problem/2231)

### 문제 풀이

1. N의 범위는 $1\le N \le1000000$  이다. 
2. N의 범위를 모두 생성자 생성 규칙을 따라가며 탐색해준다.

> 예전 풀이  


```cpp
int process(int m) {
	int sum = m;
	while (m != 0) {
		int r = m % 10;
		sum += r;
		m /= 10;
	}
	return sum;
}
void solution_2231() {
	scanf("%d", &n);
	for (int i = 1; i<=MAX; i++) {
		if (process(i) == n) {
			printf("%d\n", i);
			return;
		}
	}
	printf("0\n");
}
int main() {
	solution_2231();
	return 0;
}

```

재귀함수를 이용하여 1부터 1000000까지 모든 숫자에 대해 나머지 연산을 이용하여 생성자 규칙으로 만들어진 숫자를 주어진 N과 비교한다.  

> 이번 풀이

```cpp  
#include<cstdio>
#include<iostream>
#include<vector>
#include<string>
#include<queue>
#include<algorithm>
#include<cmath>
#define endl '\n';
#define ll long long
using namespace std;

const int MAX = 1000000;
int n;

int solution() {
	int answer = 0;
	for (int i = 1; i <= MAX; i++) {
		string tmp = to_string(i);
		answer = i;
		int order = tmp.size() - 1;
		for (int j = 0; j < tmp.size(); j++) {
			int a = tmp[j] - '0';
			answer += a;
		}
		if (answer == n)return i;
	}
}
int main() {
	ios::sync_with_stdio(false);
	cin.tie(NULL);
	cin >> n;
	cout << solution();
	return 0;
}
```
접근방식 자체는 똑같지만 이용한 방법이 다르다. 역시 1부터 1000000까지 모두 탐색하면서 정수를 문자열로 바꿔주는 `to_string()`함수를 이용하여 각 자릿수 계산을 해준다.  
  
사실 이런 to_string()함수 이런것들도 모두 구현해서 문제를 풀었었는데 사소한 예외가 많아서 문제를 틀리는 경우가 많았다. 그래서 익숙해지기 위해서 함수를 이용해 풀었지만, 위의 방식이 역시 더 마음에 든다.  
메모리와 시간 역시 더 효율적이다.  

{% include GoogleAdSenseSidebar.html %}
