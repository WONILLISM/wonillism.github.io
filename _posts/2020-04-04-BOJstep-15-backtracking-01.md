---
title: "[BOJ step 13] Brute Force 05. 영화감독 숌"
excerpt: "백준 단계별로 풀기 Brute Force 5번"

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
    - '1436'
    - 영화감독 숌
    - c++
    - cpp  
use_math: true;

last_modified_at: 2020-04-04  
---

{% include GoogleAdSenseSidebar.html %}

# [영화감독 숌](https://www.acmicpc.net/problem/1436)

처음에 뭔가 규칙이 없을까? 하고 고민을 많이해서 시간을 많이 낭비했던 문제다. 카테고리 자체가 **브루트포스** 인데 계속 문제에대해 최적화하려고 한다. **알고리즘 문제는 푸는게 목적이지 잘 푸는게 목적은 아니다** 라는걸 알고있음에도 자꾸 이상한 풀이로 빠진다. 이것 또한 노오력이 필요하겠지...  



### 문제 설명

'666' 이 연속하면서 작은 숫자부터 차례로 늘려가며 **N** 번째의 `666`이 붙은 숫자를 찾는 문제이다.  

666, 1666, 2666, 3666, 4666, ... 96662, 96663, ... 

### 문제 풀이

1. 우선 가장 작은 숫자는 `666`이므로 `answer = 666`을 해주고 `to_string(answer)`를 이용하여 숫자를 문자열로 변환해준다.
2. 문자열을 `substr`을 이용하여 3칸씩 짤라 현재 숫자에 `666`이 있는지 확인하고 있다면 `N--`를 해준다.
3. 만약 `666`이 없다면 1씩 증가시켜 다음 666이 나올때까지 반복한다.( ex. 666, 667, 668, 669, ...1664, 1665, 1666, ...)
4. 이 과정을 반복하여 **N** 이 0이되면 N번째 종말의 수 이므로 답을 출력하고 종료해준다.  


```cpp
#include <iostream>
#include <string>
#include <vector>

using namespace std;

int N;
int solution(){
	int answer = 666;
	while (1){
		string num = to_string(answer);
		for (int i = 0; i < num.size() - 2; i++){
			string tmp = num.substr(i, 3);
			if (tmp == "666"){
				N--;
				if (!N)
					return answer;
				break;
			}
		}
		answer++;
	}
	return answer;
}
int main(){
	cin >> N;
	cout << solution() << endl;
	return 0;
}
```



{% include GoogleAdSenseSidebar.html %}
