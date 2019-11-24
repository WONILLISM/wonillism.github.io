---
title: "[프로그래머스]자물쇠와 열쇠"
excerpt: "dp를 활용한 자물쇠와 열쇠"

categories:
    - Programmers
tags:
    - 프로그래머스
    - Programmers
    - 코딩테스트연습
    - 자물쇠와 열쇠
    - 알고리즘
    - 코테
    - 카카오 코딩테스트
    - kakao
    - 2020 카카오 공채
    - 2020 kakao blind recruitment
use_math: true
last_modified_at: 2019-11-24
---    
# [(lv3) 자물쇠와 열쇠](https://programmers.co.kr/learn/courses/30/lessons/60059)   

## 문제
[![](/assets/Programmers/2019-11-24-Programmers-lock-and-key-img01.png)](/assets/Programmers/2019-11-24-Programmers-lock-and-key-img01.png)  
[![](/assets/Programmers/2019-11-24-Programmers-lock-and-key-img02.png)](/assets/Programmers/2019-11-24-Programmers-lock-and-key-img02.png)  
이번 2020 카카오 공채 문제 중 하나였다. 처음 문제를 쭈욱 읽어볼 때 이건 풀 수 있겠다! 싶었는데 결국 시간이 부족해 풀지 못했다. 로직은 떠올랐는데 .....  
  
문제에 대한 로직은 다음 그림과 같다. `key`에 해당하는 배열을 회전 시켜가며 `lock`에 홈 부분에 맞는 부분이 있는지를 탐색하는 것이다.  
[![](/assets/Programmers/2019-11-24-Programmers-lock-and-key-img03.png)](/assets/Programmers/2019-11-24-Programmers-lock-and-key-img03.png)  
[![](/assets/Programmers/2019-11-24-Programmers-lock-and-key-img04.png)](/assets/Programmers/2019-11-24-Programmers-lock-and-key-img04.png)  

  
## 문제 풀이     
1. `key`를 회전시키는 함수 `Rotate()`를 구현한다  
2. `lock`에 홈의 갯수를 세어 `CNT`에 저장한다.  
3. `r`은 총 세번의 회전이 필요하므로 `r=0`일 때에는 회전시키지 않고 탐색을 한다.  
4. `key`와 `lock`이 가질 수 있는 최대값은 20 이므로 `lock`사이즈 보다 $+ 20, -20$ 만큼의 가상의 구역이 있다고 생각하고 `key`모양을 $(-20,-20)$ 부터 $(lock.size +20, lock.size + 20)$까지 한 칸 한 칸 탐색을 해준다. 
5. 탐색을 하며 `cnt`를 세고 미리 저장해둔 `CNT`와 값이 같고, 홈에 맞지않아 `fail`이 `1`이아닌 경우에는 `true`를 바로 반환하여 더 이상의 탐색은 필요 없으므로 종료한다.  
6. 만약 알맞은 홈을 찾지 못하였으면 `key`를 회전시켜 `3~5`과정을 반복한다.  

```cpp
#include <string>
#include <vector>

using namespace std;

int CNT, M, N;
vector<vector<int> > A, B;	//key, lock

void Rotate() {
	vector<vector<int> > tmp(M, vector<int>(M, 0));
	for (int i = 0; i < M; i++)
		for (int j = 0; j < M; j++)
			tmp[j][M - i - 1] = A[i][j];
	A = tmp;
}
bool solution(vector<vector<int>> key, vector<vector<int>> lock) {
	A = key; B = lock;
	M = A.size(); N = B.size();

	for (int i = 0; i < N; i++)
		for (int j = 0; j < N; j++)
			if (B[i][j] == 0)
				CNT++;

	for (int r = 0; r < 4; r++) {//?¸??
		for (int i = -20; i <= 20; i++) {
			for (int j = -20; j <= 20; j++) {
				int cnt = 0, fail = 0;
				for (int y = 0; y < M; y++) {
					for (int x = 0; x < M; x++) {
						int ny = i + y, nx = j + x;
						if (0 <= ny && ny < N && 0 <= nx && nx < N) {
							if (B[ny][nx] == 1 && A[y][x] == 1) fail = 1;
							else if (B[ny][nx] == 0 && A[y][x] == 1) cnt++;
						}
					}
				}
				if (cnt == CNT && fail == 0) return true;
			}
		}
		Rotate();
	}
	return false;
}
```
