---
title: "[Markdown] 기본 문법 정리"
excerpt: "마크다운 기본 문법을 정리해보자."

categories:
    - Make_Blog
tags:
    - Markdown 
    - Blog
last_modified_at: 2019-09-27
---

1. 텍스트 줄바꿈  
   마크다운은 줄바꿈을 인식하지 않는다.  
     
     줄바꿈을 하기 위해서는 라인 끝에 스패이스를 2번 입력해야한다.  

2. 제목 (Header)  
   html의 \<H1> ~ \<H6>와 같음
   ```
   # <H1>
   ## <H2>
   ### <H3>
   #### <H4>
   ##### <H5>
   ###### <H6>
   ```
   # This is a H1  
   ## This is a H2  
   ### This is a H3  
   #### This is a H4  
   ##### This is a H5 
   ###### This is a H6  

3. 강조 (Emphasis)  
   ```
   이텔릭체 : * 내용 * 또는 _ 내용 _
   굵게 : ** 내용 ** 또는 __ 내용 __
   이텔릭체와 굵게는 동시에 사용 가능 : **_ 내용 _**
   취소선 : <strike> 내용 </strike> , <s> 내용 </s>, <del> 내용 </del>
   밑줄 : <u> 내용 </u>
   ```
   *이텔릭체*  
   **굵게**  
   **_이텔릭체, 굵게_**  
   <del>취소선</del>  
   <u>밑줄</u>  

4. 수평규칙(Horizontal rule)
   ```
   하이픈(Hyphens) ---
   별표(Asterisks) ***
   밑줄(Underscores) ___
   ```  
   하이픈(Hyphens)  
   ---  
   별표(Asterisks)  
   ***  
   밑줄(Underscores)  
   ___  

5. 코드 블록(Code Blocks)  
   \```를 이용하여 특정 코드 또는 특정 언어 코드를 삽입 할 수 있다.  
     
   c
   ```c
   #include<cstdio>
   
   int main(){
       int a,b;
       scanf("%d%d",&a,&b);
       printf("%d%d\n",a,b);
       return 0;
   }
   ```  
   c++  
   ```cpp
   #include<iostream>
   using namespace std;
   int main(){
       int a, b;
       cin>>a>>b;
       cout<<a<<b<<endl;
       return 0;
   }
   ```

6. 인라인 코드 (Inline Code)  
   라인 안에 코드를 삽입하여 보여 준다. \'code'  
   출력 : `printf("%d");`  

7. 인용구 (Blockquotes)  
   인용구는 '>'로 시작되어 중복 사용하여 단계를 나눌 수 있다.
   ~~~
   > **<i class="fa fa-exclamation-triangle" aria-hidden="true"></i> 주의:** 이 구문은 마크다운 인용구 문법 입니다.
   > *<i class="fa fa-info-circle" aria-hidden="true"></i> 정보:* 이 구문은 마크다운 인용구 문법 입니다.
   > **<i class="fa fa-question-circle"></i> 질문:** 
   > 질문 답변입니다. 
   ~~~  
   > **<i class="fa fa-exclamation-triangle" aria-hidden="true"></i> 주의:** 이 구문은 마크다운 인용구 문법 입니다.  
   > *<i class="fa fa-info-circle" aria-hidden="true"></i> 
   정보:* 이 구문은 마크다운 인용구 문법 입니다.  
   > **<i class="fa fa-question-circle"></i> 질문:** 
   > 질문 답변입니다.   

8. 목록(List)  
   번호 매기기 목록
   1. 첫번째  
   2. 두번째
   3. 세번째
   
   블렛 목록
   '-', '*','+'를 이용, 들여쓰기를 하면 단계를 나눌 수 있다.
   - 첫번째
     - 두번째
       - 세번째

9. 이미지(Images)  
    ```
    아래와 같이 경로를 이용하여 이미지를 삽입할 수 있다.
    ![](주소)
    ```
    ![](/assets/keyboardimage.jpg)

10. 표만들기 (Table)  
    ```
    | 행렬 | 1열 | 2열 | 3열 |
    |:---:|:---:|:---:|:---:|
    | 1행 | a | b | c |
    | 2행 | 1 | 2 | 3 |
    ```
    | 행렬 | 1열 | 2열 | 3열 |  
    |:---:|:---:|:---:|:---:|  
    | 1행 | a | b | c |  
    | 2행 | 1 | 2 | 3 |  


