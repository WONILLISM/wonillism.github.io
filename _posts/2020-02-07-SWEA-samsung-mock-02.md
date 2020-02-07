---
title: "[SWEA]삼성모의기출 - 디저트 카페"
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
    - 디저트 카페
use_math: true;
last_modified_at: 2020-02-07
--- 
  
# 삼성 모의 역량 테스트  
## 문제 : [디저트 카페](https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AV5VwAr6APYDFAWu&categoryId=AV5VwAr6APYDFAWu&categoryType=CODE)  

  
## 문제설명

[![그림 1](/assets/SWEA/2020-02-07-SWEA-samsung-mock-02-img02.png)](/assets/SWEA/2020-02-07-SWEA-samsung-mock-02-img02.png)  
1. 원 안의 숫자는 디저트의 종류를 의미한다  
2. 카페 사이에는 대각선으로 이동할 수 있는 경로가 존제한다
3. 대각선 방향으로 움직여 사각형 모양을 그리며 출발한 카페로 돌아와야 한다
4. 같은 종류의 디저트는 먹을 수 없다
5. 가장 긴 경로를 찾고 그 때의 디저트 수를 출력한다  
6. 디저트를 먹을 수 없는 경우는 -1을 출력한다   
  
> __제약사항__  
> 1. 시간 제한 : 50개의 테스트를 모두 통과하는데 3초  
> 2. 지도 한 변의 크기 4 $\le$ N $\le$ 20   
> 3. 디저트 종류를 나타내는 수는 1 이상 20이하의 정수이다  

## 문제풀이  
이동경로가 상하좌우가 아닌 대각선인 __DFS or BFS__ 문제이다.  

1. 경로를 탐색하지 못하는 경우 -1을 출력해야하므로 `ans=-1`로 초기화 시킨다  
2. 디저트의 종류는 최대 20개 이므로 모든 디저트에 대한 체크를 해주는 `chk[20] = false`로 초기화 해준다  
3. 지도의 정보를 입력을 받고, 모든 좌표에 대해 __DFS__ 를 돈다. 이 때, 사각형을 그리고 다시 돌아와야 하므로 시작점의 좌표를 `sx, xy`에 담아둔다
4. `process`함수에 필요한 인자는 __탐색할 현재 위치__, __현재 진행하고 있는 방향__, __거쳐간 카페의 수__ 가 있다  
__DFS__  
5. 다음 카페로 진행할 때 두 가지 방향으로 탐색한다  
6. 다음 좌표에 해당하는 카페에 방문한적이 없다면 현재 진행방향과 같은 방향과 시계방향으로 한 번 회전한 방향에 대해서 탐색해준다.  
7. __DFS__ 를 반복하여 현재 진행 방향인 `dir=3`이고 시작점의 직전 위치인 `sx - 1, sy + 1`이면 `ans`를 최대값으로 갱신해주고 종료한다  
__/DFS__  
8. 위 과정을 반복한다  


```cpp  
#include<iostream>
#include<vector>
#include<queue>
#include<algorithm>
#define endl "\n"
using namespace std;

const int MAX = 20;
int N, ans;
int Map[MAX][MAX];
bool chk[101];
int sx, sy;//시작점
int dx[] = { 1,-1,-1,1 };
int dy[] = { 1,1,-1,-1 };

//dfs
void process(int x, int y, int dir,int step) { //좌표 x,y , 방향 
	if (dir == 3) {
		if (x == sx - 1 && y == sy + 1) {
			ans = max(ans, step);
			return;
		}
	}
	int nx = x + dx[dir], ny = y + dy[dir];
	if (nx >= 0 && nx < N&& ny >= 0 && ny < N) {
		if (!chk[Map[ny][nx]]) {
			chk[Map[ny][nx]] = true;
			process(nx, ny, dir, step + 1); //회전 안함
			process(nx, ny, dir + 1, step + 1); //회전 함
			chk[Map[ny][nx]] = false;
		}
	}
}
void solution() {
	for (int i = 0; i < N; i++) {
		for (int j = 0; j < N; j++) {
			sx = j, sy = i;
			chk[Map[i][j]] = true;
			process(j, i, 0, 1);
			chk[Map[i][j]] = false;
		}
	}
}
int main() {
	cin.tie(NULL);
	ios::sync_with_stdio(false);
	freopen("swea_2105.in", "r", stdin);
	int t; cin >> t;

	for (int tc = 1; tc <= t; tc++) {
		cin >> N;
		/*----- Init ----*/
		ans = -1;
		for (int i = 0; i < N; i++)
			for (int j = 0; j < N; j++)
				Map[i][j] = 0;
		for (int i = 0; i < 101; i++)chk[i] = false;
		/*----- Init ----*/
		for (int i = 0; i < N; i++) {
			for (int j = 0; j < N; j++) {
				cin >> Map[i][j];
			}
		}
		solution();
		cout << "#" << tc << " " << ans << endl;
	}
	return 0;
}

```
