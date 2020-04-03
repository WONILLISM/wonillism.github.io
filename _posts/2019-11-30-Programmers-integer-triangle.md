---
title: "[프로그래머스]정수 삼각형"
excerpt: "프로그래머스 코딩테스트 연습"

categories:
    - Programmers
tags:
    - 프로그래머스
    - Programmers
    - 코딩테스트연습
    - 정수삼각형
    - 알고리즘
    - 코딩
    - 코딩테스트
use_math: true
last_modified_at: 2019-11-30
published : false
---    
# [(lv3) 정수 삼각형](https://programmers.co.kr/learn/courses/30/lessons/43105)   

## 문제
[![](/assets/Programmers/2019-11-30-Programmers-integer-triangle-img01.jpg)](/assets/Programmers/2019-11-30-Programmers-integer-triangle-img01.jpg)  
이 문제 역시 `dp`를 활용하자.   
경로의 방향은 `(0,0) -> (1,0) or (1,1) ` 이런 식으로 배열로 생각한다면 아래 또는 오른쪽 아래로 내려갈 수 있다.  
끝까지 내려가는 경로 중 가장 큰 값을 출력하는 문제이다.
## 문제 풀이  
[![](/assets/Programmers/2019-11-30-Programmers-integer-triangle-img02.jpg)](/assets/Programmers/2019-11-30-Programmers-integer-triangle-img02.jpg)   
한 점으로 올 수 있는 경우의 수는 2가지이다. 2가지 경로 중 큰 값을 찾아 `DP`배열에 해당 점의 값과 더하여 넣어준다.  
이 과정을 진행하면서 최하단의 값들은 이전의 값들 보다 작을 수 없으므로 연산을 진행하면서 모든 경우의 최대값을 비교해주며 찾아준다.  
연산과정에서 가장 왼쪽과 오른쪽에 대한 값들은 경우의 수가 계속해서 한 가지 이므로 `i=0`(해당 행의 가장 왼쪽) , `i=n`(해당 행의 가장 오른쪽)의 값들은 그냥 이전의 값과 누적해서 `DP`에 넣어준다.  

```cpp
#include <iostream>
#include <string>
#include <vector>
using namespace std;
vector<vector<int>> T;
int dp[500][500];
int Max;
int process(int n,int idx) {
	if (idx < 0)return 0;
	if (n == 0)return dp[0][0] = T[0][0];

	if (dp[n][idx])return dp[n][idx];
	else {
		int a = process(n - 1, 0);
		for (int i = 0; i <=n; i++) {
			//int b = process(n - 1, i - 1);
			if (i == 0) {
				dp[n][i] = a + T[n][i];
			}
			else if(i>0&&i<n){
				int b = process(n - 1, i);
				int c = a > b ? a : b;
				dp[n][i] = c + T[n][i];
				a = b;
			}
			else if (i == n) {
				dp[n][i] = a + T[n][i];
			}
			if (Max < dp[n][i])Max = dp[n][i];
		}
		return dp[n][idx];
	}
}
int solution(vector<vector<int>> triangle) {
	T = triangle;
	process(triangle.size() - 1, 0);
	int answer = Max;
	return answer;
}
```  

