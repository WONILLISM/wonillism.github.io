---
title: "[SWEA]삼성모의기출 - 보호 필름"
excerpt: "삼성 모의 기출 문제 풀이"

categories:
    - SWEA
tags:
    - SWEA
    - Samsung Expert Academy
    - 삼성코테
    - 코딩테스트
    - 알고리즘
    - 삼성모의기출
    - 보호필름
use_math: true;
last_modified_at: 2020-02-07
published : false
--- 
  
# 삼성 모의 역량 테스트  
## 문제 : [보호 필름](https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AV5V1SYKAaUDFAWu&categoryId=AV5V1SYKAaUDFAWu&categoryType=CODE&&&)  
  
  
## 문제설명
1장 당 각 셀들이 __특성 A__ 와 __특성 B__ 로 이루어진 보호필름을 D장 쌓아서 제작 된다. 
[![그림 1](/assets/SWEA/2020-02-07-SWEA-samsung-mock-03-img01.png)](/assets/SWEA/2020-02-07-SWEA-samsung-mock-03-img01.png)  
  
가로의 길이는 W이며 __단면의 모든 세로방향에 대해서 동일한 특성의 셀들이 K개 이상 연속적으로 있는경우 성능검사를 통과 한다__  

  

> __제약사항__  
> 1. 시간 제한 : 50개의 테스트를 모두 통과하는데 3초  
> 2. 보호 필름의 두께 3 $\le$ D $\le$ 13   
> 3. 보호 필름의 가로크기 1 $\le$ W $\le$ 20  
> 4. 합격 기준 K 1 $\le$ K $\le$ D  
> 5. 셀이 가질 수 있는 특성은 A,B만 존재  

## 문제풀이  
약품 투여를 좀 더 효율적으로 할 수 있는 방법은 없을까? 에 대한 고민을하다가 시간 제한이 넉넉해서 그냥 __Brute Force__ 를 했다.  
  
1. 약품 투여 횟수가 최소인 경우가 답이므로 높이의 최대값으로 초기화 해준다. `ans =13`  
2. 깊이가 0이고 약품 투여 횟수가 0을 시작으로 바로 __DFS__ 를 시행해 준다.  
3. `process`함수에 필요한 인자는 __현재 탐색하고 있는 레이어의 깊이__, __현재까지 약품을 투여한 횟수__  
__DFS__  
4. 각각의 열에 대해서만 탐색하면 되므로 방문체크를 해주는 것이 아니라 약품 투여 여부를 깊이에 대해서만 해주는데 이 때, 투여 __했다, 안했다__ 만 체크하는 것이 아니라 투여 __안했다(-1), A투여(0), B투여(1)__ 로 체크해준다  
5. 위 세 가지 투여 여부를 이용하여 탐색을 한다.  
   ```cpp  
   chk[depth] = -1;
	process(depth + 1, cnt);//투여 안함
	chk[depth] = 0;
	process(depth + 1, cnt + 1);//a 투여
	chk[depth] = 1;
	process(depth + 1, cnt + 1);//b 투여

   ```
6. 만약 `cnt` 횟수가 `ans`값 보다 크거나 같으면 이미 최솟값은 구한 것이므로 더 이상 탐색하지 않는다  
7. 만약 `depth`값이 `D`보다 커지면 필름의 높이만큼 모두 탐색했으므로 보호필름의 각 레이어에 `chk[]`에 표시된 약품 투여 여부를 확인하여 약품 투여 후 합격 여부를 판단한다.  
8. 만약 합격이라면 ans값을 최솟값으로 갱신해준다.  
__/DFS__  
9. 위 과정을 반복한다
  

```cpp  
#include<iostream>
#include<vector>
#include<queue>
#include<algorithm>
#define endl "\n"
using namespace std;

int D, W, K, ans;
int Map[13][20];
int Tmp[13][20];
int chk[13]; // 약품 투여 여부

// 성능 검사
bool check() {
	int cnt;
	for (int i = 0; i < W; i++) {
		cnt = 1;
		for (int j = 1; j < D; j++) {
			if (cnt >= K)break;
			if (Tmp[j - 1][i] == Tmp[j][i])cnt++;
			else cnt = 1;
		}
		if (cnt < K)return false;
	}
	return true;
}
// dfs - 약품 종류, 깊이, 약품 투여 횟수
void process(int depth, int cnt) {
	if (cnt>=ans)return;
	if (depth > D) {
		for (int i = 0; i < D; i++) {
			for (int j = 0; j < W; j++) {
				if (chk[i] != -1) {
					Tmp[i][j] = chk[i];
				}
				else Tmp[i][j] = Map[i][j];
			}
		}

		if (check()) 
			ans = min(ans, cnt);
		return;
	}
	chk[depth] = -1;
	process(depth + 1, cnt);//투여 안함
	chk[depth] = 0;
	process(depth + 1, cnt + 1);//a 투여
	chk[depth] = 1;
	process(depth + 1, cnt + 1);//b 투여
}
void solution() {
	process(0, 0);
}
int main() {
	cin.tie(NULL);
	ios::sync_with_stdio(false);
	freopen("swea_2112.in", "r", stdin);
	int t; cin >> t;

	for (int tc = 1; tc <= t; tc++) {
		cin >> D >> W >> K;
		/*----- Init ----*/
		ans = 13;
		for (int i = 0; i < D; i++) {
			for (int j = 0; j < W; j++) {
				cin >> Map[i][j];
			}
		}
		solution();
		cout << "#" << tc << " " << ans << endl;
	}
	return 0;
}
```
