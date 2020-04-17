---
title: "[BOJ step 14] 정렬 1 ~ 6"
excerpt: "백준 단계별로 풀기 정렬 문제 1 ~ 6"

categories:
    - BOJ_Step
tags:
    - 알고리즘
    - algorhtim
    - BOJ
    - '2750'
    - '2751'
    - '10989'
    - '2108'
    - '1427'
    - 정렬
    - sorting
    - BOJ step
    - 단계별로풀기
    - step 14
    - c++
    - cpp  
use_math: true;

last_modified_at: 2020-04-17  
---

# 정렬(Sorting)  

### $O(n^2)$
+ [선택정렬](https://ko.wikipedia.org/wiki/%EC%84%A0%ED%83%9D_%EC%A0%95%EB%A0%AC)  
[![](/assets/Algorithm/Selection-Sort-Animation.gif)](/assets/Algorithm/Insertion-sort.gif)  
+ [삽입정렬](https://ko.wikipedia.org/wiki/%EC%82%BD%EC%9E%85_%EC%A0%95%EB%A0%AC)  
[![](/assets/Algorithm/Insertion-sort.gif)](/assets/Algorithm/Insertion-sort.gif)  
+ [거품정렬](https://ko.wikipedia.org/wiki/%EA%B1%B0%ED%92%88_%EC%A0%95%EB%A0%AC)  
[![](/assets/Algorithm/Bubble-sort.gif)](/assets/Algorithm/Bubble-sort.gif)  
  
### $O(n \log n)$  
+ [퀵정렬](https://ko.wikipedia.org/wiki/%ED%80%B5_%EC%A0%95%EB%A0%AC) : 평균적으로($O(n\log n)$, 최악의 경우($O(n^2)$)
[![](/assets/Algorithm/Quick-sort.gif)](/assets/Algorithm/Quick-sort.gif)  
+ [병합정렬](https://ko.wikipedia.org/wiki/%ED%95%A9%EB%B3%91_%EC%A0%95%EB%A0%AC)   
[![](/assets/Algorithm/merge-sort.gif)](/assets/Algorithm/merge-sort.gif)  
  
> 참조 : 위키백과  


## [수 정렬하기](https://www.acmicpc.net/problem/2750)  

선택정렬을 이용한 풀이  

```cpp  
#include<iostream>
#include<algorithm>
#include<vector>
#define endl '\n'
using namespace std;

int main() {
	ios::sync_with_stdio(false);
	cin.tie(NULL);

	int n; cin >> n;
	vector<int> v(n);
	for (int i = 0; i < n; i++)
		cin >> v[i];
	for (int i = 0; i < n; i++) {
		int m_idx = i;
		for (int j = i + 1; j < n; j++) 
			if (v[j] < v[m_idx]) m_idx = j;
		int tmp = v[m_idx];
		v[m_idx] = v[i];
		v[i] = tmp;
	}
	
	bool chk = false;
	for (int i = 0; i < v.size(); i++) {	
		if (!chk) {
			chk = true;
			cout << v[i] << endl;
		}
		else {
			if (v[i - 1] != v[i])chk = false;
			if (!chk) {
				chk = true;
				cout << v[i] << endl;
			}
		}
	}
	return 0;
}
```

  

## [수 정렬하기 2](https://www.acmicpc.net/problem/2751)  

C++ `<algorithm>` 에 있는 `sort()` 함수 역시 merge sort 기반으로 알고있다. 직접 구현한 코드를 이용한 풀이이다.  

```cpp
#include<cstdio>
int D[1000000];
int Tmp[1000000];
void MergeSort(int start, int end, int *data) {
	int i = start;
	int k = start;
	int m = (start + end) / 2;
	int j = m + 1;
	if (start >= end)return;	// 더 이상 분할할수없음.
	MergeSort(start, m, data);	// 쪼개기 왼쪽
	MergeSort(m + 1, end, data);// 쪼개기 오른쪽
	while ((i <= m) && (j <= end)) {	// 비교 후 정렬
		if (data[i] < data[j])Tmp[k++] = data[i++];
		else Tmp[k++] = data[j++];
	}
	while (i <= m)Tmp[k++] = data[i++];	// 남은 부분 정렬
	while (j <= end)Tmp[k++] = data[j++];
	for (i = start; i <= end; i++)data[i] = Tmp[i];	// 교환
}
int main() {
	int n;
	scanf("%d", &n);
	for (int i = 0; i < n; i++)scanf("%d", &D[i]);
	MergeSort(0, n - 1, D);
	for (int i = 0; i < n; i++)printf("%d\n", D[i]);
	return 0;
}
```

  

## [수 정렬하기 3](https://www.acmicpc.net/problem/10989)  

카운팅 정렬을 이용한 풀이  

적은 범위가 주어진다면 범위만큼의 배열을 만들어 배열 인덱스를 수로 활용한다.  

```cpp
#include<cstdio>
int D[10001];
int main() {
	int n, a;
	scanf("%d", &n);
	for (int i = 0; i < n; i++) {
		scanf("%d", &a);
		D[a]++;
	}
	for (int i = 0; i < 10001; i++) {
		for (int j = 0; j < D[i]; j++) {
			printf("%d\n", i);
		}
	}
	return 0;
}
```

​    

## [통계학](https://www.acmicpc.net/problem/2108)  

위의 정렬방법들을 이용하여 풀이  

```cpp
#include<cstdio>
#include<algorithm>
using namespace std;
int Num[500000];
int Tmp[500000];
int Cnt[8001];
int Max;
int main() {
	int n, sum = 0;
	scanf("%d", &n);
	for (int i = 0; i < n; i++) {
		scanf("%d", &Num[i]);
		sum += Num[i];
		Cnt[Num[i] + 4000]++;
		if (Max < Cnt[Num[i] + 4000])Max = Cnt[Num[i] + 4000];
	}
	sort(Num, Num + n);
	int j = 0, frq;
	for (int i = 0; i < 8001; i++) {
		if (Cnt[i] == Max) {
			frq = i - 4000;
			j++;
			if (j == 2) {
				frq = i - 4000;
				break;
			}
		}
	}
	printf("%.0f\n", sum / (double)n);
	printf("%d\n", Num[n / 2]);
	printf("%d\n", frq);
	printf("%d\n", Num[n - 1] - Num[0]);
	return 0;
}
```



## [소트인사이드](https://www.acmicpc.net/problem/1427)  

string 정렬을 이용한 역순 출력

```cpp
#include<iostream>
#include<string>
#include<algorithm>
using namespace std;

bool comp(char a, char b) { return a > b; }
int main() {
	ios::sync_with_stdio(false);
	cin.tie(NULL);
	cout.tie(NULL);

	string s;
	cin >> s;
	sort(s.begin(), s.end(), comp);
	cout << s;
	return 0;
}
```

  

## [좌표정렬하기](https://www.acmicpc.net/problem/1427)  

sort함수와 우선순위 큐를 이용한 풀이  

```cpp
#include<iostream>
#include<vector>
#include<queue>
#include<algorithm>
#define PII pair<int, int>
#define endl '\n'

using namespace std;

typedef struct pos {
	int x, y;
}Pos;
bool operator<(const Pos &a, const Pos &b) {
	if (a.x != b.x)return a.x > b.x;
	else return a.y > b.y;
}
priority_queue<Pos> pq;
int main() {
	ios::sync_with_stdio(false);
	cin.tie(NULL);
	cout.tie(NULL);
	vector<PII> v;
	int n; cin >> n;
	while (n--) {
		int x, y;
		cin >> x >> y;
		v.push_back({ x,y });
	}
	sort(v.begin(), v.end());
	for (PII ans : v) {
		cout << ans.first << " " << ans.second << endl;
	}
	return 0;
}
```

  

```cpp
#include<iostream>
#include<vector>
#include<queue>
#include<algorithm>
#define PII pair<int, int>
#define endl '\n'

using namespace std;

typedef struct pos {
	int x, y;
}Pos;
bool operator<(const Pos &a, const Pos &b) {
	if (a.x != b.x)return a.x > b.x;
	else return a.y > b.y;
}
priority_queue<Pos> pq;
int main() {
	ios::sync_with_stdio(false);
	cin.tie(NULL);
	cout.tie(NULL);

	int n; cin >> n;
	while (n--) {
		Pos tmp;
		cin >> tmp.x >> tmp.y;
		pq.push(tmp);
	}
	while (!pq.empty()) {
		Pos cur = pq.top();
		pq.pop();
		cout << cur.x << " " << cur.y << endl;
	}
	return 0;
}
```



{% include GoogleAdSensePost.html %}