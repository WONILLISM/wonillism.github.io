---
title: "[Algorithm] 자료구조 해시(Hash)"
excerpt: "자료구조 hash를 알아보자"

categories:
    - Algorithm
tags:
    - hash
    - hash map
    - hash table
    - data structure
    - 해시
    - 해쉬
    - 해시 맵
    - 해시 테이블
    - 해쉬 맵
    - 해쉬 테이블
    - 자료구조
    - '14501'
    - c++
    - cpp  
use_math: true;

last_modified_at: 2020-03-27
--- 

자료구조 **Hash** 에 대해 알아보자. 평소 알고리즘을 풀 때 크게 신경쓰지 않았던 자료구조다. 그냥 구조체로 선언해서 비슷하게 구현하면서 문제를 풀었던 것 같다.  
`<set>`, `<map>` 등의 cpp 컨테이너들의 존재는 알고있었지만 **STL** 을 여러개 사용하는 것에 대해 익숙하지 않아서 안썼었다. 근데 막상 써보니 너무 편리했다.   

하지만 항상 명심하자 **STL** 을 사용할 때는 사용법을 정확하게 알고 문제에 적용시킬 수 있을 때 사용하자. 

{% include GoogleAdSenseSidebar.html %}

# Hash(해시) 란?  

이전에 소개했던 [c++ STL이란?](https://wonillism.github.io/c++_stl/cppSTL/) 포스팅에서 언급했던 연관 컨테이너들과 관련이있다.  

**해시 테이블(hash table)** , **해시 맵(hash map)** 등 이들은 **key** 를 **값** 에 매핑할 수 있는 구조인, **연관 배열** 추가에 사용되는 자료구조이다.  

**해시(hash)** 를 이용하면 데이터의 검색과 저장을 매우 빨리 할 수 있다.

### 연관 배열 (associative array)이란?

**키(key)** 1개 와 **값(value)** 1개가 1:1로 연관되어 있는 구조이다. 따라서 **키(key)** 를 이용하여 **값(value)** 를 도출할 수 있다.  

### 해시 테이블의 구조  
[![](/assets/cppSTL/hashtable.png)](/assets/cppSTL/hashtable.png)
> 출처 : [위키 백과](https://en.wikipedia.org/wiki/Hash_table)  

+ **키(key)** : 고유한 값이며, 해시 함수의 input이 된다. 다양한 길이의 값이 될 수 있으므로 해시 함수로 값을 바꾸어 저장 되어야 공간 효율성을 추구 할 수 있다.  
+ **해시 함수(hash function)** : **키(key)** 를 일정한 길이를 가지는 **해시(hash)** 로 변경하여 저장소를 효율적으로 운영할 수 있도록 도와준다. 다만, 서로 다른 **키(key)** 가 같은 **해시(hash)** 가 되는 경우( **해시 충돌(hash collision)**  를 최대한 줄이는 함수를 만드는 것이 중요하다.  
+ **해시(hash)** : **해시 함수(hash function)** 의 결과물이며, **저장소(bucket, slot)** 에서 **값(value)** 과 매칭되어 저장된다.  
+ **값(value)** : **저장소(bucket, slot)** 에 최종적으로 저장되는 값으로 키와 매칭되어 저장, 삭제, 검색, 접근이 가능해야 한다.

후에 해시와 관련된 컨테이너들을 포스팅 하겠다.

{% include GoogleAdSenseSidebar.html %}