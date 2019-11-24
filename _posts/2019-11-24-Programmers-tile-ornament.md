---
title: "[프로그래머스]타일 장식물"
excerpt: "dp를 활용한 타일 장식물"

categories:
    - Programmers
tags:
    - 프로그래머스
    - Programmers
    - 코딩테스트연습
    - 타일 장식물
    - DP
    - 동적프로그래밍
    - memoization
    - 메모이제이션  
use_math: true
last_modified_at: 2019-11-24
---    
# [(lv3) 타일 장식물](https://programmers.co.kr/learn/courses/30/lessons/43104)   

## 문제
[![](/assets/Programmers/2019-11-24-Programmers-ornaments-img01.png)](/assets/Programmers/2019-11-24-Programmers-ornaments-img01.png)  
원리 자체는 `2xn타일링`문제와 동일하다. 
  
## 문제 풀이  
첫 번째와 두 번째를 제외하고 한 변의 길이가 일정한 규칙을 가지며 증가하고 있다.   
[![](/assets/Programmers/2019-11-24-Programmers-ornaments-img02.png)](/assets/Programmers/2019-11-24-Programmers-ornaments-img02.png)  
  
위 그림과 같이 $f(1)$과 $f(2)$를 제외하고 $f(3)$부터 이전의 사각형의 둘레에 그 이전의 사각형의 둘레만큼 더하는 규칙을 찾을 수 있다.  
따라서 점화식으로 표현하면  
$f(n) = f(n-1) + f(n-2)$ 라고 할 수 있다.  
```cpp
using namespace std;

long long dp[81];
long long solution(int n) {
	if (n == 1)return dp[n] = 4;
	else if (n == 2)return dp[n] = 6;
	if (dp[n]) return dp[n];
	else {
		dp[n] = solution(n - 1) + solution(n - 2);
		return dp[n];
	}
}
```
