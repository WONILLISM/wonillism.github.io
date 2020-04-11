---
title: "[BOJ step 5] 실습 1"
excerpt: "백준 단계별로 풀기 실습 1"

categories:
    - BOJ_Step
tags:
    - brute force
    - 알고리즘
    - algorhtim
    - BOJ
    - '1436'
    - '10039'
    - '5543'
    - '10817'
    - '2523'
    - '2446'
    - '10996'
    - c++
    - cpp  
use_math: true;

last_modified_at: 2020-04-04  
---

{% include GoogleAdSenseSidebar.html %}

# [실습 1](https://www.acmicpc.net/step/48)  
또 변경 예정일지는 모르겠지만 단계별로 풀기 **완료** 도장을 찍고싶었다... 
그리 어렵지 않은 문제들이라 큰 설명은 하지 않겠다.
  
## [01. 평균 점수](https://www.acmicpc.net/problem/10039)  
  

```cpp
#include<stdio.h>
int n, sum;
int main() {
	for (int i = 0; i < 5; i++) {
		scanf("%d", &n);
		if (n <= 40)n = 40;
		sum += n;
	}
	printf("%d", sum / 5);	
	return 0;
}
```  
  
## [02. 평균 점수](https://www.acmicpc.net/problem/10039)  
  

```cpp
#include<iostream>
#include<algorithm>

using namespace std;

int main() {
	int arr[5], answer = 1 << 30;
	for (int i = 0; i < 5; i++)
		cin >> arr[i];

	for (int i = 0; i < 3; i++)
		answer = min(arr[i] + arr[3] - 50, min(arr[i] + arr[4] - 50, answer));
	cout << answer << endl;
	return 0;
}
```  
  

## [03. 세 수](https://www.acmicpc.net/problem/10817)  
  

```cpp
#include<cstdio>
int main() {
	int a, b, c;
	scanf("%d%d%d", &a, &b, &c);
	printf("%d", a > b ? (a > c ? (b > c ? b : c) : a) : (b > c ? (a > c ? a : c) : b));
}
```

## [04. 별 찍기 - 13](https://www.acmicpc.net/problem/2523)  
  
두 가지 방법으로 풀어보았다. 처음엔 그냥 윗 부분 아랫 부분으로 나누어 2중 for문을 두 번 썼다. 좀 비효율적이라고 생각되서 최적화할 방법을 생각해봤다.  

```cpp  
#include<iostream>
using namespace std;
int main() {
	ios::sync_with_stdio(false);
	cin.tie(NULL);
	cout.tie(NULL);

	int n; cin >> n;

	for (int i = 0; i < n; i++) {
		for (int j = 0; j <= i; j++) {
			cout << "*";
		}
		cout << endl;
	}
	for (int i = 0; i < n - 1; i++) {
		for (int j = 0; j < n - i - 1; j++) {
			cout << "*";
		}
		cout << endl;
	}

	return 0;
}
```  
  
문제는 별의 개수가 증가하다가 감소하는 형태이므로 증가 값을 `k`로 두고 `i`를 중가시키다가 `i > n-1`이 되면 `k=-`로 바궈주어 다시 i를 감소시켜준다.  
  
```cpp
#include<cstdio>
int main() {
	int n, k = 1;
	scanf("%d", &n);
	for (int i = 1; i > 0; i += k) {
		for (int j = 0; j < i; j++) printf("*");
		printf("\n");
		if (i > n - 1) k *= -1;
	}
}
```  
  
{% include GoogleAdSensePost.html %}  
  

## [05. 별 찍기 - 9](https://www.acmicpc.net/problem/2446)  
  
이 문제 역시 두 가지 방법으로 풀어보았다.   

```cpp  
#include<iostream>

using namespace std;

int main() {
	ios::sync_with_stdio(false);
	cin.tie(NULL);
	cout.tie(NULL);

	int n; cin >> n;
	int star = 2 * n - 1;
	int blank = 0;
	for (int i = 0; i < 2 * n - 1; i++) {
		for (int j = 0; j < blank; j++)
			cout << " ";
		for (int j = 0; j < star; j++)
			cout << "*";
		cout << endl;


		if (i >= n-1) {
			blank--;
			star += 2;
		}
		else{
			blank++;
			star -= 2;
		}
	}
	return 0;
}
```  

```cpp  
#include<iostream>

using namespace std;

int main() {
	ios::sync_with_stdio(false);
	cin.tie(NULL);
	cout.tie(NULL);
	int n; cin >> n;

	for (int i = 1; i <= 2 * n - 1; i++) {
		int k = (i <= n) ? i : 2 * n - i;
		for (int j = 1; j <= k - 1; j++) cout << " ";
		for (int j = k; j <= 2 * n - k; j++) cout << "*";
		printf("\n");
	}
	return 0;
}
```
  
## [06. 별 찍기 - 10996](https://www.acmicpc.net/problem/10996)  
  

```cpp  
#include<iostream>

using namespace std;

int main() {
	ios::sync_with_stdio(false);
	cin.tie(NULL);

	int n; cin >> n;
	for (int i = 0; i < 2 * n ; i++) {
		for (int j = 0; j < n; j++) {
			if (i % 2 == 0) {
				if (j % 2 == 0)printf("*");
				else printf(" ");
			}
			else {
				if (j % 2 == 0)printf(" ");
				else printf("*");
			}
		}
		puts("");
	}
	return 0;
}
```  

{% include GoogleAdSensePost.html %}
