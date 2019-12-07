---
title: "[프로그래머스]예산"
excerpt: "프로그래머스 코딩테스트 연습"

categories:
    - Programmers
tags:
    - 프로그래머스
    - Programmers
    - 코딩테스트연습
    - 예산
    - 알고리즘
    - 코딩
    - 코딩테스트
use_math: true
last_modified_at: 2019-12-07
---    
# [(lv3) 예산](https://programmers.co.kr/learn/courses/30/lessons/43237)   

## 문제
[![](/assets/Programmers/2019-12-02-Programmers-budgets-img01.jpg)](/assets/Programmers/2019-12-02-Programmers-budgets-img01.jpg)   
각 지방의 예산을 정해진 국가 예산의 총액 이하에서 가능한 한 최대의 예산을 배정하는 방법의 문제다.  
상한액을 기준으로 예산들이 큰지 작은지를 비교해가며 상한액을 구하는 방법인데 인덱스를 기준으로 `이분 탐색`을 한 것이 아니라 상한액을 기준으로 `이분 탐색`을 하여 문제를 해결했다.  

## 문제 풀이  
1. 주어진 지방 예산들을 오름차순 정렬한다.  
2. 각 지방의 예산을 모두 더해서 예산의 총합(`sum`)과 국가 예산 `M`을 비교한다
3. 만약 `sum <= M` 이라면 지방 예산들 중 가장 큰 금액이 상한액이므로 `budgets[size-1]`를 반환한다.  
4. 그렇지 않다면 가능한 한 최대의 예산을 배정하기 위한 방법을 구한다.   
`avg = sum/size` 지방 예산들의 합을 지방 수로 나눈 `avg`
`avg1 = M/size` 국가 예산을 지방 수로 나눈 `avg1` -> 상한액
+ 만약 상한액보다 `i`번째 지방 예산이 더 크다면 지방 예산 만큼 배정할 수 없으므로 상한액을 배정한다.
+ 그렇지 않다면 지방 예산을 배정하고 배정한 지방 예산을 국가 예산에서 빼주고 상한액(`(M - sum1)/size`)을 다시 구한다.
5.  위 과정을 예산이 상한액보다 커지는 경우가 될때까지 반복한다.  



```cpp
#include <iostream>
#include <vector>
#include<algorithm>
using namespace std;
int solution(vector<int> budgets, int M) {
	int size = budgets.size();
	long long sum = 0;
	sort(budgets.begin(), budgets.end());
	for (int i = 0; i < size; i++)
		sum += budgets[i];
	if (sum <= M)return budgets[size - 1];
	long long sum1 = 0;
	long long avg1 = M / size;

	for (int i = 0; i < budgets.size(); i++) {
		if (budgets[i] > avg1)return avg1;
		sum1 += budgets[i];
		size--;
		avg1 = (M - sum1) / size;
	}
}

``` 

