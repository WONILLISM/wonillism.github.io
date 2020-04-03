---
title: "[c++STL] algorithm"
excerpt: "`<algorithm>`에 대해서 알아보자."

categories:
    - C++_STL
tags:
    - C++
    - STL
    - 표준라이브러리
    - 알고리즘
    - <algorithm>
last_modified_at: 2020-03-27
published : false
---
# 2019-09-03 updated

## `<algorithm>`이란?  
알고리즘 라이브러리는 컨테이너에 반복자들을 가지고 이런 저런 작업들을 쉽게 수행할 수 있도록 도와주는 라이브러리이다.  

{% include GoogleAdSenseSidebar.html %}

***
STL 알고리즘은 한쌍의 반복자 `[begin,iter),(iter,end]` 를 구간으로 갖는다.  
대부분의 알고리즘은 순방향 반복자를 요구한다.  

### STL 알고리즘의 분류
+ 원소를 수정하지 않는 알고리즘(nonmodifying algorithms)  
+ 원소를 수정하는 알고리즘(modifying algorithms)  
+ 제거 알고리즘(removing algorithms)
+ 변경 알고리즘(mutating algorithms)
+ 정렬 알고리즘(sorting algorithms)
+ 정렬된 범위 알고리즘(sorted range algorithms)
+ 수치 알고리즘(numeric algorithms)

### find 알고리즘 예시
컨테이너는 `<vector>`를 이용하자.
```c++
#include<iostream>
#include<vector>
#include<algorithm>

using namespace std;

int main(){
    vector<int> v;
    v.push_back(11);
    v.push_back(22);
    v.push_back(33);
    v.push_back(44);
    v.push_back(55);

    vector<int>::iterator iter; // 반복자만 생성
    /* 반 개구간 [begin, end)에서 33을 찾아 iter에 대입하라 */ 
    iter = find(v.begin(), v.end(), 33);
    cout << *iter << endl;

    iter = find(v.begin(), v.end(), 66);
	if (iter == v.end())  // 만약 반복자가 모두 순회를 했는데 찾지 못했으면
		cout << "not found" << endl;
	else cout << *iter << endl;

    return 0;
}
```

STL을 공부하기 전 `<algorithm>`도 다른 컨테이너와 같은 줄 알았는데 살짝 공부해보니 아닌 것 같다.  
이번 주는 9/7일에 있을 카카오 코딩 테스트 때문에 자세히 알아보는 것은 다음으로 미루고 다른 컨테이너에 대해서 
좀 더 알아보자.  

  {% include GoogleAdSensePost.html %}

# 2020-03-27 Updated  

자주 사용하는 `<algorithm>` 컨테이너의 **함수** 를 알아보자. 

### sort 함수  

아마 c에서 c++로 넘어오면서 가장 많이 사용하는 함수가 아닐까 싶다. 예전에는 정렬을 해야할 일이 있으면 **merge sort** 를 직접 구현해서 문제를 풀었었다. 구조를 이해하고 있으면 그리 어렵지 않게 외워지지만 매번 정렬할때마다 구현하는 것이 여간 짜증나는게 아니었다.  

```cpp  
//머지소트(Merge Sort)
void MergeSort(int data[], int start, int end) {
	int tmp[MAX_Q];
	int i = start;
	int k = start;
	int m = (start + end) / 2;
	int j = m + 1;
	if (start >= end) return; //쪼갤수 없음, 되돌아가기
	MergeSort(data, start, m); //분할
	MergeSort(data, m + 1, end); //분할
	while ((i <= m) && (j <= end)) { //병합
		if (data[i] < data[j]) tmp[k++] = data[i++];
		else tmp[k++] = data[j++];
	}
	while (i <= m) tmp[k++] = data[i++]; //나머지 병합
	while (j <= end)  tmp[k++] = data[j++]; //나머지 병합
	for (i = start; i <= end; i++) data[i] = tmp[i]; //복사
}
```

결코 짧지않은 소스 코드이다. 하지만 자료형의 제한도 있고 여간 불편한게 아니다. c++의 컨테이너인 **algorithm** 안에 있는 **sort** 함수를 이용하면 한 줄에 끝날 일을...  

```cpp  
#include<algorithm>
#include<vector>
#include<string>

using namespace std;

int main(){
    vector<int> v = {3,2,9,1,2,4}; 
    sort(v.begin(), v.end()); // 1,2,2,3,4,9
    string s = "wonil";
    sort(s.begin(), s.end());	// ilnow    
    return 0;
}
```



숫자 뿐만 아니라 문자도 정렬이 가능하다. 문자열도 가능하다!(사전식으로) 

```cpp	
sort([start, end), 정렬방식(default : 오름차순));
```

개구간 start에서 폐구간 end 까지 정렬방식에 의해 정렬이 가능하다.  정렬방식은 `bool`함수를 만들어 원하는데로 정렬이 가능하다.  

```cpp
bool cmp(int a, int b){ return a < b;}	// 오름차순
bool cmp(int a, int b){ return a > b;} // 내림차순

sort(v.begin(), v.end(), cmp);
```



### max, min 함수  

간단히 구현할 수 있는 함수이지만 이것 역시 자주 쓰인다.  

```cpp  
int a = 10, b = 20;
int res = max(a,b);	// 20
int res = min(a,b); // 10
```



