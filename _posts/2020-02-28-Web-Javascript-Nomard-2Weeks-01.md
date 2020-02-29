---
title: "[Javascript] vanillaJS 2주완성 01"
excerpt: "vanillia JS로 크롬 앱 만들기"

categories:
    - WEB
tags:
    - javascript
    - 자바스크립트
    - vanilla JS
    - vanilla
    - 웹 개발
    - 프론트 엔드
    - front end
use_math: true;
last_modified_at: 2020-02-28
--- 
> __HTML/CSS__ 공부  
> 개발 언어 : __javascript__  
> 개발 환경 : __Visual studio Code__  
> 강의 : [Vanillia JS 2주 완성반 with Nomard](https://academy.nomadcoders.co/courses/enrolled/435558)  
  
# 01_Hello World!  
  
외부 js파일 받아오기  
+ `html`의 `<body>`~`</body>`의 가장 마지막부분에  
`<script src="js파일 경로"></script>`    
를 입력해야한다.
  
`html파일`  
```html  
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Hello World!</title>
    <link rel="stylesheet" href="./index.css">
</head>
<body>
    <h1>Hello World!</h1>

    <script src="./index.js"></script>
</body>
</html>
```  
  
`js파일`  
```js  
alert("Hello world!");
```  
  
[![그림 01](/assets/web/nomard-js-2weeks/2020-02-28-Web-Javascript-Nomard-2Weeks-01-img01.png)](/assets/web/nomard-js-2weeks/2020-02-28-Web-Javascript-Nomard-2Weeks-01-img01.png))  
  
## 변수 type  
  
+ __var__ : ES6 이전 버전에서 쓰이던 변수. 중복 선언이 가능하다. 따라서 코드의 길이가 길어지면 에러를 발생시킬수 있는 가능성이 커진다.  
+ __let__ : `var`과 같은 변수이지만, 중복 선언이 불가능하다. `var`의 단점을 보완해서 ES6 이후 추가되었다.  
+ __const__ : 중복 선언이 불가능하고, 재할당도 불가능하다. 말그대로 상수이다.  
+ `let`과 `const`를 이용하여 `boolean`, `string`도 선언가능하다.  
  
> __※ Camel case__  
> 나도 모르게 사용하고 있던 변수 선언 방식  
> 간혹 변수 이름을 정하다보면 공백이 필요한 경우가 있는데 그때 `_`(under bar)나 대문자로 구분하곤 했는데 대문자로 구분하던 방식이 Camel case이다.  
> 낙타 등 처럼 변수 이름의 첫 문자는 소문자로 시작하고 공백이나 구분짓는 부분이 필요하다면 대문자로 구분지어주는 방식
  
## 배열(Array)  

`const daysOfWeek = ["Mon","Tue","Wed","Thu","Fri","Sat","Sun",true];`  
위와 같이 선언할 수 있는데 변수 type은 구애받지 않는다.  
물론 인덱스로 접근도 가능하다.  
`console.log(daysOfWeek);` -> `["Mon","Tue","Wed","Thu","Fri","Sat","Sun",true]`  
`console.log(daysOfWeek[0]);` -> `Mon`  

## 객체(Object)  
> `javascript`의 객체 선언이 꽤나 흥미롭다.  
> c++, java 처럼 class 선언이 아닌 그냥 배열 선언 처럼 `square bracket(대괄호)` 대신  `bracket(중괄호)`를 이용하여 선언한다.  
  
```js  
const wonieeInfo ={
    name: "Woniee",
    gender: "Male"
    isHandsome: true;
}
  
wonieeInfo.isHandsome = false;  
```  
`const`로 선언했지만 객체 안의 변수들은 재할당이 가능하다. 하지만 객체 자체의 변경은 불가능하다.  
> 음..?  
  
## 함수와 객체 섞어쓰기  
```js  
const calculator = {
    plus : function(a,b){
        return a+b;
    }
}

const plus = calculator.plus(2,5);
consol.log(plus);   // 7
```  



