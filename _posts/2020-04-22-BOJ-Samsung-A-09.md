---
title: "[삼성코테기출문제] 다리만들기 2"
excerpt: "삼성sw역량테스트 A형 기출문제 9"

categories:
    - 삼성기출문제
tags:
    - 다리만들기2
    - BOJ17472
    - 알고리즘
    - algorhtim
    - 백준
    - 삼성
    - A형
    - 기출
    - 코딩테스트
    - 코테
    - SW역량테스트
    - c++
    - cpp  
last_modified_at: 2020-04-22  
---  
# [다리만들기2](https://www.acmicpc.net/problem/17472)  
{% include GoogleAdSensePost.html %}  
이거 A형 기출 맞아??? 하면서 풀었다. 막상 풀고나서 문제를 이해해보면 그리 어렵지는 않지만 시험장에서 푼다면.. 자신없다.   
  
문제를 해석해보면 주어지는 **지도 정보**를 **간선 정보**로 변환하여 **최소신장트리(MST)** 를 사용하여 답을 출력하라는 문제다.  
  

## 문제    
[![](/assets/BOJ-samsung/2020-04-22-BOJ-Samsung-A-09-img01.png)](/assets/BOJ-samsung/2020-04-22-BOJ-Samsung-A-09-img01.png)  
  

## 문제 풀이  
1. 우선 문제에서
  
__풀이 과정__  
  
{% include GoogleAdSensePost.html %}  

```cpp
#include<iostream>
#include<queue>
#include<vector>
#include<map>
#include<algorithm>
#define PII pair<int,int>

using namespace std;

const int MAX = 10;
int N, M;
int Map[MAX][MAX];
int visit[MAX][MAX];
bool island[6];
int ans;
int dy[] = { -1,0,1,0 };
int dx[] = { 0,1,0,-1 };

queue<pair<PII, int>> startPos;	// 시작 좌표, 시작 섬 넘버
struct node { int cost, u, v; };
vector<node> g;
vector<int> p;	// 부모노드 표시
map<PII, int> nodeInfo;

bool comp(node a, node b) { return a.cost < b.cost; }
bool isRanged(int y, int x) { return y >= 0 && y < N && x >= 0 && x < M; }
void initVisit() {
	for (int i = 0; i < N; i++)
		for (int j = 0; j < M; j++)
			visit[i][j] = 0;
}
void numbering(int y, int x, int num) {		// 섬 넘버링
	queue<PII> q;
	q.push({ y,x });
	visit[y][x] = 1;
	Map[y][x] = num;
	while (!q.empty()) {
		PII cur = q.front();
		q.pop();
		
		for (int i = 0; i < 4; i++) {
			int ny = cur.first + dy[i];
			int nx = cur.second + dx[i];

			if (isRanged(ny, nx) && !visit[ny][nx]) {
				if (Map[ny][nx]) {
					visit[ny][nx] = 1;
					Map[ny][nx] = num;
					q.push({ ny,nx });
				}
				else {	// 다리 이을 시작 좌표 
					startPos.push({ {cur.first, cur.second }, num });
				}
			}
		}
	}
}
void linkIsland(int y, int x, int cnt, int dir, int num) {
	int ny = y + dy[dir];
	int nx = x + dx[dir];
	if (isRanged(ny, nx)) {
		if (!Map[ny][nx]) {
			visit[ny][nx] = 2;
			linkIsland(ny, nx, cnt + 1, dir, num);
		}
		else {
			if (cnt > 1) {			
				PII key;
				if(num<Map[ny][nx])key = { num, Map[ny][nx] };
				else key = { Map[ny][nx],num };
				if (nodeInfo.find(key) == nodeInfo.end()) {
					nodeInfo[key] = cnt;
				}
				else nodeInfo[key] = min(nodeInfo[key], cnt);
			}
		}
	}
}
int _find(int x) {
	if (p[x] == x)return x;
	else return p[x] = _find(p[x]);
}
void _union(int u, int v) {
	u = _find(u);
	v = _find(v);
	if (u != v)p[u] = v;
}
bool isSameParent(int u, int v) {
	u = _find(u);
	v = _find(v);
	if (u == v)return true;
	else return false;
}
void solution() {
	int num = 0;
	for (int i = 0; i < N; i++) {
		for (int j = 0; j < M; j++) {
			if (Map[i][j] == 1 && !island[num] && !visit[i][j]) {
				island[num] = true;
				numbering(i, j, num + 1);
				num++;
			}
		}
	}
	while (!startPos.empty()) {
		pair<PII, int> cur = startPos.front();
		startPos.pop();
		int y = cur.first.first;
		int x = cur.first.second;
		int n = cur.second;

		for (int i = 0; i < 4; i++) {
			int ny = y + dy[i];
			int nx = x + dx[i];
			if (isRanged(ny,nx)&&visit[ny][nx]!=1) {
				visit[ny][nx] = 2;		//다리 연결시 중복 방문 가능
				linkIsland(ny, nx, 1, i, n);
			}
		}
	}
	
	if (nodeInfo.size() < num - 1) {
		cout << -1 << endl;
		return;
	}
	// kruskal
	for (int i = 0; i <= num; i++) p.push_back(i);
	for (auto ret : nodeInfo) 
		g.push_back({ ret.second,ret.first.first,ret.first.second });

	sort(g.begin(), g.end(), comp);
	
	for (int i = 0; i < g.size(); i++) {
		int u = g[i].u, v = g[i].v, c = g[i].cost;
		if (!isSameParent(u, v)) {
			_union(u, v);
			ans += c;
		}
	}
	int cnt = 0;
	for (int i = 1; i < p.size(); i++) 
		if (p[i] == i)cnt++;
	if (cnt > 1)cout << -1 << endl;
	else cout << ans << endl;
}
int main() {
	ios::sync_with_stdio(false);
	cin.tie(NULL);
	cout.tie(NULL);
	freopen("a_09.in", "r", stdin);

	ans = 0;
	cin >> N >> M;

	for (int i = 0; i < N; i++) {
		for (int j = 0; j < M; j++) {
			cin >> Map[i][j];
			visit[i][j] = 0;
		}
	}
	solution();
	return 0;
}
```