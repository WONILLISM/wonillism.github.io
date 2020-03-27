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
---
## `<algorithm>`이란?  
알고리즘 라이브러리는 컨테이너에 반복자들을 가지고 이런 저런 작업들을 쉽게 수행할 수 있도록 도와주는 라이브러리이다.  

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