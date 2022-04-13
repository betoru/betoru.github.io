---
layout: post
date: 2022-04-13 22:17:00 +0900
title: 'JavaScript: VanillaJs-DOM-#3-function'
category:
  - script language
tags:
  - script language
  - javascript
  - vanillaJS
  - function
  - json
img: js-1.png # Add image post (optional)  
---

* Kramdown table of contents    
{:toc .toc}

### 함수와 표현식
> 함수를 정의한다는 것은 실행 전 사전지식으로 표현할 수 있다.   
자바스크립트는 함수를 정의하지 않고 만든다고 한다.

```javascript
    //일반적인 함수
    int add(int x, int y){
        return x+y;
    }
    
    //자바스크립트 함수 표현식
    var add = new Function("x,y","return x+y");
    document.write("------- 1 --------");
    document.write("<br/>");
    document.write(add(5,4))

    //자바스크립트의 유연성으로 표현식은 이렇게 달리할 수 있다.
    var adds = function(x,y){
        return x+y;
    };
    document.write("------- 2 --------");
    document.write("<br/>");
    document.write(adds(5,4))

    //심지어 이렇게도 표현할 수 있음.
    function addss(x,y){
        console.log(arguments.length);//collection, arguments
        return x+y;
    }
    document.write("------- 3 --------");
    document.write("<br/>");
    document.write(addss(6,4));

    //자바스크립트는 특이하게 매개변수(parameter)가 의미가 없다.
    //매개변수는 값을 받는 그릇으로써 역할을 하지 않는다.
    //자바스크립트는 데이터가 다 객체이기 때문에 매개변수 x,y는 참조하는 이름일뿐이다.
    //인자(arguments)들은 가변적으로 collection에 쌓이게 된다. 
    var sum = addss(12,3,5,6,7);
    document.write("------- 4 --------");
    document.write("<br/>");
    document.write(sum);
```
