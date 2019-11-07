---
title: "[c++] sort() 함수"
excerpt: "c++ STL의 sort() 함수를 알아보자"

categories:
    - C++_STL
tags:
    - C++
    - STL
    - 표준라이브러리
    - 알고리즘
    - 정렬
    - sort
    - 자료구조
last_modified_at: 2019-11-06
---  
자료구조에는 여러가지 정렬 방법이 있다. 그 정렬 방법에따라 시간 복잡도는 `O(n^2)`, `O(nlogn)`등으로 나뉜다.  
[![](/assets/cppSTL/sort.gif)](/assets/cppSTL/sort.gif)
##### 출처 : <http://www.todayhumor.co.kr/board/view.php?table=bestofbest&no=200940>  
정렬에 대해 구글링을 하다가 우연히 발견한 gif이다. 모든 정렬들의 속도를 비교하며 한눈에 볼 수 있어서 매우 좋은 것 같다.  
<https://www.toptal.com/developers/sorting-algorithms> 여기서 직접 하나씩 실행 할 수 있다.  
  
많은 정렬 방법들이 있지만 알고리즘 문제를 풀 때 직접 작성하지 않고 c++ STL에 내장되어있는 sort()함수에 대해서 알아보자.  

## sort() 함수란?  
__sort()__ 함수는 `<algorithm>`에 정의되어있다.  
```cpp
// < 를 이용한 비교 (1)
template <class RandomIt>
void sort(RandomIt first, RandomIt last);

// 비교 함수 (comp) 를 이용한 비교 (2)
template <class RandomIt, class Compare>
void sort(RandomIt first, RandomIt last, Compare comp);

// Execution policy 를 지정한 경우 (3)
template <class ExecutionPolicy, class RandomIt>
void sort(ExecutionPolicy&& policy, RandomIt first, RandomIt last);

template <class ExecutionPolicy, class RandomIt, class Compare>
void sort(ExecutionPolicy&& policy, RandomIt first, RandomIt last,
          Compare comp);
```  
  

  +  (1)의 경우 주로 vector 와 자주 쓰이며, 배열인 경우도 시작과 끝을 알고있다면 사용할 수 있다. 기본 설정 값은 `first`부터 `last`까지 오름차순으로 정렬한다.  
  ```cpp  
  vector<int> a;
  sort(a.begin(), a.end());
  ```  
  + (2)의 경우 비교함수를 이용하여 정렬  
  ```cpp
  vector<int> a;
  bool compare(const Type1 &a, const Type2 &b){
    return a < b;
  }    
  sort(a.begin(), a.end(), compare);
  ```  
  매개변수 두 개를 받아 비교하여, 첫 번째 인자가 더 작을 경우 true를 리턴해야 한다. 굳이 `const&` 일 필요는 없지만, 함수 내부에서 인자로 받은 원소를 수정하면 안된다.  
  + (3), (4)의 경우 (1), (2)와 동일하지만, 어떠한 방식으로 실행할 지 지정할 수  있다. 해당 함수가 오버로드 되기 위해서는 `std::is_execution_policy_v<std::decay_t<ExecutionPolicy>>` 가 참이어야 한다.  
  + `first`와 `last` 는 임의 접근 반복자(RandomIterator) 여아한다. 따라서 list의 경우 순차 접근 반복자 이므로 sort() 함수로 정렬을 수행할 수 없다.  

## 실행 복잡도  
평균적으로 O(NlogN)으로 실행된다.  
  
## 실행 예제  
```cpp
#include <algorithm>
#include <array>
#include <functional>
#include <iostream>

int main() {
  std::array<int, 10> s = {5, 7, 4, 2, 8, 6, 1, 9, 0, 3};

  // operator< 를 사용해 정렬
  std::sort(s.begin(), s.end());
  for (auto a : s) {
    std::cout << a << " ";
  }
  std::cout << '\n';

  // 표준 라이브러리 비교 함수 객체 greater 를 통한 정렬
  std::sort(s.begin(), s.end(), std::greater<int>());
  for (auto a : s) {
    std::cout << a << " ";
  }
  std::cout << '\n';

  // 함수 객체를 이용한 정렬
  struct {
    bool operator()(int a, int b) const { return a < b; }
  } customLess;
  std::sort(s.begin(), s.end(), customLess);
  for (auto a : s) {
    std::cout << a << " ";
  }
  std::cout << '\n';

  // 람다 함수를 이용한 정렬
  std::sort(s.begin(), s.end(), [](int a, int b) { return a > b; });
  for (auto a : s) {
    std::cout << a << " ";
  }
  std::cout << '\n';
}
```  

##### 참조 : <https://modoocode.com/272>
