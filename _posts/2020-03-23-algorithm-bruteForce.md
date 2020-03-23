---
title: "[Algorithm] Brute Force"
excerpt: "Brute Force를 알아보자"

categories:
    - Algorithm
tags:
        - brute force
            - 브루트 포스
            - 완전탐색
            - 야만적인 힘
            - 알고리즘
            - algorhtim
            - 개념  
use_math: true;

last_modified_at: 2020-03-23
--- 

# Brute Force Search(브루트포스)  

아마도 알고리즘을 공부하면서 가장 처음으로 뭔가... 알고리즘 같은? 것을 배우기 시작하는 부분이 아닐까 싶다.  

흔히들 그냥 브루트 포스라고 부르지만 알고리즘이므로 **Search** 가 붙는 것이 맞다고 본다.  

   

**Brute Force(브루트 포스)** : 야만적인 힘  

즉, 무식하게 모든 경우를 다 탐색해본다는 뜻이다. 모든 경우를 다 탐색하는 만큼 거의 틀릴 일 없이 정확하다. 하지만, 그만큼 많은 **시간복잡도** 와 **공간복잡도** 를 갖는다.  

작년 이맘때 즈음 알고리즘 공부를 시작하면서 무작정 부딪혔을때가 생각난다. 상반기 시즌이 얼마 남지 않았어서 속성으로 공부하고 있을때여서 확실한 이해도 없이 문제를 풀었었던... 간단한 문제들 조차 며칠씩 걸려서 문제를 풀고 너무 힘들었던 ... ㅠㅜ (지금도 힘들다.)  

당시에 풀었던 문제를 리뷰해보자.  

## [일곱 난쟁이](https://www.acmicpc.net/problem/2309)  

**문제 요약**  

100을 넘지않는 9개의 정수가 주어지고 9개 중 7개의 정수의 합이 100이 되는 경우를 찾아 그 7개의 정수를 출력하라.  

  

**문제 설명**  
$_9C_7$ 이 되는 모든 경우의 수를 구하여라.  

즉, 9명의 난쟁이 중 키의 합이 100이 되는 7명을 찾아라. 라는 문제이다.  

  

**문제 풀이**  

예전 코드  

```cpp  
#include<iostream>

using namespace std;

const int MAX_HEIGHT = 100;

int dwarf[9];

int Sum;

void Input() {
	for (int i = 0; i < 9; i++) {
		cin >> dwarf[i];
		Sum += dwarf[i];
	}
}

void Find7Dwarfs(int i, int j) {
	int find7 = Sum - (dwarf[i] + dwarf[j]);
	
	if (MAX_HEIGHT == find7) {
		dwarf[i] = -1;
		dwarf[j] = -1;
		return;
	}

	if (j == 8) {
		i++;
		j = i + 1;
	}
	else j++;

	Find7Dwarfs(i, j);
}
void Swap(int *a, int *b) {
	int t = *a;
	*a = *b;
	*b = t;
}
void QuickSort(int left, int right, int *data) {
	int pivot = left;
	int j = pivot;
	int i = left + 1;

	if (left < right) {
		for (; i <= right; i++) {
			if (data[i] < data[pivot]) {
				j++;
				Swap(&data[j], &data[i]);
			}
		}
		Swap(&data[left], &data[j]);
		pivot = j;
		QuickSort(left, pivot - 1, data);
		QuickSort(pivot + 1, right, data);
	}
}
void Process() {
	Find7Dwarfs(0, 1);
	QuickSort(0, 8, dwarf);
	for (int i = 2; i < 9; i++)
		cout << dwarf[i] << endl;
}
void Solution() {
	Input();
	Process();
}

int main() {
	Solution();
	return 0;
}
```

와... 이 때는 알고리즘 잘하는 친구 왈 "stl 쓰지말라!" 는 한 마디에 모든걸 구현해서 풀었다.. c와 c++은 그냥 printf, scanf 이냐 cin cout이냐 밖에 없다...  

예전 알고리즘 문제들은 stl을 사용하지 못하게하는 시험들이 많았다라고는 했었는데.. 1년의 경험상 무쓸모다 쓸 수있는 stl은 쓰자! 대신 구조와 작동방식은 정확하게 알고 가자.  

  

대충 기억을 더듬어 보면 재귀함수를 이용하여 모든 경우를 구했다.   

1. 9개의 정수를 입력 받으며 전체 합을 구한다.  
2. 9개 중 2개씩 선택하며 선택한 두 수를 총 합에서 빼고 100인지 확인한다.  
3. 그림 설명.  

![그림 설명1](/assets/Algorithm/2020-03-23-algorithm-bruteforce-img01.png)  

4. 위 그림과 같이 i와 j를 하나씩 증가해주면서 조건에 맞는 결과를 찾을 때 까지 반복한다.  



**dp** 나 **좀 더 최적화 시킬 방법** 을 찾다가 문제 자체가 그냥 완탐을 하라는 문제인거 같아서 고민하다가 그냥 완전탐색으로 구현하였다. 그리 복잡한 문제도 아니고 해서 재귀를 사용하지 않고 반복문으로 해결하였다.  

```cpp
#include<iostream>
#include<vector>
#include<algorithm>
using namespace std;

int main() {
	vector<int> v;
	int sum = 0;
	for (int i = 0; i < 9; i++) {
		int a; cin >> a;
		v.push_back(a);
		sum += a;
	}
	vector<int> answer;
	for (int i = 0; i < 9; i++) {
		for (int j = i + 1; j < 9; j++) {
			if (sum - v[i] - v[j] == 100) {
				for (int k = 0; k < 9; k++) {
					if (k != i && k != j) {
						answer.push_back(v[k]);
					}
				}
				sort(answer.begin(), answer.end());
				for (auto ans : answer)
					cout << ans << endl;
				return 0;
			}
		}
	}
	
	return 0;
}
```

