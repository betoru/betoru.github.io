---
layout: post
date: 2022-04-13 23:17:00 +0900
title: 'JavaScript: VanillaJs-DOM-#4-clouser'
category:
  - script language
tags:
  - script language
  - javascript
  - vanillaJS
  - clouser
  - json
img: js-1.png # Add image post (optional)  
---

* Kramdown table of contents    
{:toc .toc}

### 변수의 가시영역과 전역변수

```javascript
    //var 선언 변수는 정적인 방식으로 생성된다.
    //코드 순서에 따라 상태를 살펴보자.
    var a = 5;      //키워드 : A
    console.log(a); //키워드 : B
    /*
        순서
            1. A -> B : 5 출력
            2. B -> A : undefined(=변수는 선언했으나 값을 할당하지 않은 상태. 즉, 자료형이 없는 상태 *null은 빈값이 할당된 상태(빈객체))
                그럼 왜 undefined 인가? 참조변수는 만들어졌으나 값이 할당되지 않은 상태. 다시말해 순서에 의해 값은 할당된다.
     */

    //전역변수(global)는 동적인 방식으로 생성된다.
    //var는 변수를 선언하는 키워드이며 생략해도 출력이 되며, 이때 전역객체로 window를 호출하여 선언된다.
    //ex)window.b 이런 경우 순서를 바꾸면 에러가 나온다. (Uncaught ReferenceError: b is not defined)
    b = "b의값입니다";   //키워드 : A
    console.log(b);    //키워드 : B

    //전역변수 window.d = 1; 지역변수 var d = 2; 생성 후 값 증가
    //어느 변수의 값이 증가될까? => 함수 내 우선순위는 지역변수에 있다. *위치를 변경해도 결과는 동일
    var f1 = function(){
        d = 1;
        var d = 2;
        d++;    
        return d;
    };
    console.log(f1());

    //동일한 변수를 여러번 선언해도 에러는 없으며 마지막 참조변수에 참조됨.
    var e = 1;
    var e = 2;
    console.log("e : "+e);
    
    //중괄호 내 선언된 변수는 밖에서 사용할 수 없는건데 자바스크립트는 예외
    //단, 함수 내 지역변수는 제외.
    { var f = 1; }
    console.log("f : "+ f);
    
    //함수 안에서 선언한 local, global 변수
    //지역변수는 defined 노출, 전역변수는 정상노출
    function f2(){
        var g = 1;
        // g = 1; //전역객체
        // return g;
    }
    f2();
    console.log("g : "+g);
    
    //클로저(clouser)
    //JS는 함수 내 함수 선언가능
    //자바스크립트는 함수를 정의하지 않고 객체로 만들어 그 자체가 정의다 라고 생각하면 된다.
    //함수를 객체로 만들기 때문에 그 객체가 반환될 수 있고, 함수 내 함수가 만들어질 수 있고
    //그러다보니 함수가 가지고 있는 지역변수가 클로저라는 것을 낳을 수 있다.
    function f3(){
        var h = 3;
        f4();
        function f4(){
            var h = 4;
            f5();
            function f5(){
                var h = 5;
            }
        }
    }
    console.log("f3 함수 시작");
    f3();
    // console.log("h : "+h);    
    
    function f6()
    {//block start : 지역변수의 유효범위 시작
        var i = 1;
        return i;
    }//block end : 지역변수의 유효범위 끝
    
    //f6 함수가 호출되고 함수내 지역변수i는 사라짐. 여기에 i의 변수는 호출함수 값을 참조한다.
    var i = f6();
    console.log("i : "+i);
    
    /**
     * 그런데 만일 위처럼 값을 참조하는게 아니라 함수를 참조한다면?
     *  1.함수f7 내 지역변수 j 객체를 만들고 1의 값을 참조하도록 한다.
     *  2.함수f8을 리턴하도록한다. 함수블록 끝
     *  3.변수k 객체를 만들어 f7함수를 참조하도록 한다.
     *  4.변수k는 함수 객체를 참조하므로 함수로 호출이 가능하고 그 값을 j 변수가 참조하도록 한다.
     *  문제는 없는가?
     *  3번에서 변수k가 f7함수를 참조하고 호출되어 f7함수는 f8함수를 리턴했으니 지역변수 j를 삭제하고 끝나야한다.
     *  근데 f8함수가 함수 지역변수 j를 참조하고 리턴하려고 한다.
     *  f8이 사용유무에 따라 j를 삭제해야할지 유지해야할지 JS는 판단해야한다.
     *  결론은 삭제되지 않고 유지한다.
     *  이때 f8은 f7의 클로저 함수가 된다.
     *  클로저 함수는 의도하고 사용하면 좋지만 그렇지않으면 자원낭비나 에러를 만들어낼 수 있다.
     */
    function f7(){
        var j = 1;
        return function f8(){
            return j;
        }
    }
    
    var k = f7();
    var j = k();
    console.log("클로저 j : "+j);
```
