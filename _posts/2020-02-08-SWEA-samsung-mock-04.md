---
title: "[SWEA]삼성모의기출 - 미생물 격리"
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
    - 미생물 격리
use_math: true;
last_modified_at: 2020-02-08
--- 
  
# 삼성 모의 역량 테스트  
## 문제 : [미생물 격리](https://swexpertacademy.com/main/talk/solvingClub/problemView.do?solveclubId=AWvQZwwaOT0DFAW4&contestProbId=AV597vbqAH0DFAVl&probBoxId=AXAXx6CquiIDFARP&type=PROBLEM&problemBoxTitle=2020+%EC%82%BC%EC%84%B1+%EB%AA%A8%EC%9D%98+%ED%85%8C%EC%8A%A4%ED%8A%B8&problemBoxCnt=5)  
  
  
## 문제설명
N * N 정사각형 구역 안에 K개의 미생물 군집이 있다.  
미생물들이 구역을 벗어나는 것을 방지하기 위해 가장 바깥쪽 가장자리 부분의 셀들에는 특수한 약품이 칠해져 있다.  
  
[![그림 1](/assets/SWEA/2020-02-08-SWEA-samsung-mock-04-img01.png)](/assets/SWEA/2020-02-08-SWEA-samsung-mock-04-img01.png)  
  
1. 최초 각 미생물 군집의 위치, 군집 내 미생물의 수, 이동 방향이 주어진다. 약품이 칠해져 있는 부분에는 미생물이 배치 되어 있지 않다.  
2. 각 군집들은 1시간마다 이동방향에 있는 다음 셀로 이동한다.  
3. 약품이 칠해진 곳에 미생물 군집이 도착하면 
   1. 군집 내 미생물 수 / 2 (나머지는 버림)
   2. 미생물 수 = 0  이면 군집은 사라짐
4. 두 개 이상의 군집이 하나의 셀에 모이는 경우 합쳐진다.
   1. 이동방향은 미생물 수가 많은 군집에 의해 결정
   2. 미생물 수가 같은 경우는 고려하지 않아도 됨
  
M 시간 후에 남아있는 미생물 수를 구하라.  
    

> __제약사항__  
> 1. 시간 제한 : 50개의 테스트를 모두 통과하는데 5초  
> 2. 구역의 모양 정사각형 한 변의 길이 5 $\le$ N $\le$ 100   
> 3. 최초 미생물 군집의 수  5 $\le$ K $\le$ 1000  
> 4. 격리 시간  1 $\le$ M $\le$ 1000  
> 5. 최초에 둘 이상의 군집이 동일한 셀에 존재하지 않음
> 6. 각 군집의 미생물의 수 10000 이하
> 7. 군집의 이동방향 (1:상, 2:하, 3:좌, 4:우)  
> 8. 각 군집의 정보 : 세로, 가로, 미생물 수, 이동방향 순으로 주어짐.  

## 문제풀이  
`19년 상반기 기출문제인 [낚시왕](https://www.acmicpc.net/problem/17143)과 조금 비슷한 것 같다. 당시 상반기 역량테스트를 치뤘지만 알고리즘을 시작하지 1달 정도 밖에 되지 않았던 터라 너무 어려웠었다. 아직 풀진 않았지만 조만간 이 문제도 풀어볼 예정이다.  
  
우선 미생물 군집을 동시에 어떻게 움직일 것인지를 결정하는 하는 것부터 시작했다.  
큐에 담아서 하나씩 꺼내며 이전 정보를 어딘가에 저장해 두고 다음 정보에 한꺼번에 갱신하는 방법으로 문제를 해결하다가 자꾸 조건이 꼬여서 다른 방법을 생각했다.  
최초 미생물 군집의 정보가 주어지므로 주어지는 미생물 정보를 저장해두고 갱신해가며 문제를 해결했다.  
  
1. 미생물 군집 정보를 받기 위해 `vector<int> v`를 초기화 해주고 군집의 번호를 1부터 시작하기 위해 `v.push_bakc({0,0,0,0});`을 해준 뒤 미생물 군집 정보를 입력 받는다.    
2. 미생물 군집의 인덱스 정보와 해당 좌표의 미생물 수를 저장하는 `Map[][][2]`의 모든 값을 0으로 초기화 해준다.  
3. 살아있는 모든 미생물 군집에 대하여 조건들을 처리해준다.  
4. 해당 미생물 군집의 미생물 수가 0이 아니라면 살아 있으므로 미생물 군집이 살아있는 경우에 다음 조건들을 처리한다. 
5. 현재 군집의 방향으로 다음 좌표를 입력받고 다음 좌표가 약품처리된 구역이라면 군집의 방향을 반대로 바꾸고, 미생물 수를 반감 시켜준다.  
6. 다음 좌표에 다른 군집이 없다면 해당 좌표의 맵에 현재 군집의 인덱스와 수를 저장한다.  
7. 다음 좌표에 다른 군집이 있다면 해당 좌표의 인덱스를 받아 해당 인덱스의 군집에 현재 군집의 미생물 수를 더해준다.  
8. 만약 맵에 저장되어있는 군집의 미생물 수 보다 현재 군집의 미생물 수가 더 많다면 다음 좌표에 저장되어있는 미생물의 수를 현재 군집의 미생물 수로 바꿔주고 해당 군집의 방향도 현재 군집의 방향으로 바꾸어 준다.  
9. 처리가 완료되면 해당 맵에 저장되어 있던 군집의 정보를 바꿔주었으므로 현재 군집의 미생물의 수를 0으로 바꿔준다.  
10. 2 ~ 9의 과정을 M시간동안 반복해준다.  
  
  
```cpp  
#include<cstdio>
#include<iostream>
#include<vector>
#include<string>
#include<queue>
#include<algorithm>
#define endl '\n';
#define ll long long
#define PII pair<int,int>
using namespace std;

const int MAX = 101;
int ans, N, M, K;
struct Micro {
	int y, x, n, dir;	// 위치, 수, 방향;
};
int Map[MAX][MAX][2];	// 미생물 군집 인덱스 정보와 좌표의 미생물의 수

int dx[] = { 0,0,0,-1,1 };
int dy[] = { 0,-1,1,0,0 };
int convDir[] = { 0,2,1,4,3 };// 상>하, 하>상, 좌>우, 우>좌
vector<Micro> v;

bool isEdge(int y, int x) { return x == 0 || x == N - 1 || y == 0 || y == N - 1; }
void solution() {
	while (M--) {
		fill(&Map[0][0][0], &Map[N - 1][N - 1][0], 0);
		fill(&Map[0][0][1], &Map[N - 1][N - 1][1], 0);
		for (int i = 1; i <= K; i++) {
			Micro &mic = v[i];

			//미생물 수가 0이 아니면 살아있는 군집
			if (mic.n) {
				int ny = mic.y + dy[mic.dir], nx = mic.x + dx[mic.dir];
				mic.y = ny;
				mic.x = nx;
				//경계에 닿았을 때 처리 
				if (isEdge(ny, nx)) {
					mic.dir = convDir[mic.dir];
					mic.n /= 2;
				}
				// 다음 좌표에 미생물이 없으면
				if (!Map[ny][nx][0]) {
					Map[ny][nx][0] = i;
					Map[ny][nx][1] = mic.n;
				}
				// 다음 좌표에 미생물이 있으면
				else {
					int idx = Map[ny][nx][0];
					v[idx].n += mic.n;

					// 해당 좌표의 군집보다 더 많으면 자신의 방향으로 바꾸고 미생물 수도 바꾼다.
					if (Map[ny][nx][1] < mic.n) {
						Map[ny][nx][1] = mic.n;
						v[idx].dir = mic.dir;
					}
					//처리가 완료되면 미생물을 사라지게함.
					mic.n = 0;
				}
			}
		}
	}
	
	for (int i = 1; i <= K; i++) ans += v[i].n;
}
int main() {
	cin.tie(NULL);
	ios::sync_with_stdio(false);
	freopen("swea_2382.in", "r", stdin);

	int t; cin >> t;
	for (int tc = 1; tc <= t; tc++) {
		cin >> N >> M >> K;
		/*--- Init ---*/
		ans = 0;
		v.clear();

		/*--- Input ---*/
		v.push_back({ 0,0,0,0 });
		for (int i = 0; i < K; i++) {
			int y, x, n, dir;
			cin >> y >> x >> n >> dir;
			v.push_back({ y,x,n,dir});
		}
		solution();
		cout << "#" << tc << " " << ans << endl;
	}

	return 0;
}
```
