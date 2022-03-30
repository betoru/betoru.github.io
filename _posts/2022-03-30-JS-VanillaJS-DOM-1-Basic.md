---
layout: post
date: 2022-03-30 22:17:00 +0900
title: 'JavaScript: VanillaJs-DOM-#1-Basic'
category:
  - script language
tags:
  - script language
  - javascript
  - vanillaJS
  - dom
  - json
img: js-1.png # Add image post (optional)  
---

* Kramdown table of contents
{:toc .toc}

### Goal of learning
Script language의 기본인 Javascript의 바닐라JS의 개념, 구조 등을 다시 공부하여 
한줄의 코드를 작성함에도 유의미하게 생각할 수 있도록 한다.
좋은 코드, 즉 기능성,효율성 협업을 고려한 코드를 작성하는 것에 목표를 둔다.
이후, 객체지향과 ES6 등 학습범위를 넓히고 새로운 스크립트 언어로 확대하기로 한다.

### 환경준비
- vscode
- chrome
- live server

### 데이터
#### 변수 키워드 var
```javascript
var x = 3;          //정수
var x = 3.6;        //실수
var x = 'A';        //문자
var x = "Hello";    //문자열
```
타입은 익히 알고있어 넘어간다하더라도 궁금한게 하나 생긴다.  
*어떻게 변동되는 타입에 공간을 할당받는거지?*  
=> 자바스크립트는 변수 선언시 공간을 마련하지 않는다.
자바스크립트 변수는 참조변수로 값이 할당되는 시점에 공간을 갖는다.
이를 'Auto Boxing'이라 표현한다.  
포인터(주소를 저장하는 변수)가 아닌 참조(reference)를 의미한다.  
강아지에게 강아지라 부르지 않고 이름을 붙이는 것처럼 변수는 이름을 붙이는 것.
자바스크립트의 변수는 모두 참조변수이며 Wrapper class를 가지고 있다.  

```javascript
//변수 선언에 대한 표현으로 생성자 함수 키워드인 new를 생략할 수 있다.
//JS의 유연함을 볼 수 있다.
var x = 3;
var x = new Number(3);
```
위의 코드를 프로그램 언어에서는 _변수x에 3을 할당했다. 혹은 3으로 선언했다. 초기화했다._ 표현하지만
자바스크립트는 _3의 데이터가 담긴 wrapper class를 x 라는 이름으로 참조한다._ 라고 표현하는게 올바르다. 
타입은 데이터를 보고 결정한다. 해당 타입을 체크하기 위해 typeof 연산자를 쓴다. 
JS의 유연성은 장점이면서 동시에 단점이 된다. 어떤 타입의 변수인가에 따라 사용할 수 있는 함수가 변경되기 때문이다.

#### Array 객체
```javascript
//push, pop method를 이용한 데이터 관리 : stack
var nums = new Array();
nums.push(5);
nums.push(10);
nums.push(20);
/*
    적재(stack) 형태로 데이터가 쌓임.
    20
    10
    5
    pop을 이용, 데이터를 꺼내면 적재된 최신 순서부터 꺼내오며 꺼낸 데이터는 사라진다.
 */
var n1 = nums.pop(); // 20
var n2 = nums.pop(); // 10
var n3 = nums.pop(); // 5
```
```javascript
//index를 이용한 데이터관리 : List
var nums = new Array();
nums[0] = 5;
nums[1] = 10;
nums[2] = 20;
//pop과 달리 값을 꺼내도 사라지지 않는다.
alert(nums[0]);//5
```
```javascript
/*
    배열 선언방법
    다른 언어에서는 같은 타입의 데이터를 목록화 하는데,
    JS는 다른 타입의 데이터도 가능하다.
    단일한 값으로 제한하지 않아 배열 내 배열도 선언할 수 있다.
 */
var num = new Array(5); //5개의 공간
var num = new Array(5,10,21); //3개의 공간에 데이터
var num = new Array(5,10,21, "hello"); //타입체크는 typeof를 이용** 
var num = new Array(5,10,21, "hello", new Array(2,3,4)); 
nums[4][1]; // 배열 내 배열의 데이터 호출 시 : 3
```
```javascript
//splice() 메소드를 이용한 데이터 관리 : List
var nums_splice = new Array(5,10,21,"hello", 33, 44, 55);

//(n) index n 이후 값 삭제
nums_splice.splice(1); 

//(n,m) index n번째 부터 m개 인자 삭제
nums_splice.splice(3,4); 

//(n,m,a) index n번째 부터 m개 인자 삭제하고 n번째 index에 a값 추가
nums_splice.splice(2,0,"hi"); 
console.log(nums_splice);
```
#### Object 객체
```java
/* 
    자바에서 클래스와 객체(Object) 인스턴스 차이
    1. 클래스 생성(정의) 
    2. 클래스의 객체 생성 
    3. 클래스의 인스턴스 생성(객체를 메모리에 할당) 
 */
 public class Animal {
 ...
 }
 //객체와 인스턴스
 public class Main {
     public static void main(String[] args) {
         Animal cat, dog; // '객체'

         // 인스턴스화
         cat = new Animal(); // cat은 Animal 클래스의 '인스턴스'(객체를 메모리에 할당)
         dog = new Animal(); // dog은 Animal 클래스의 '인스턴스'(객체를 메모리에 할당)
     }
 }
```
```javascript
/* 
    자바스크립트에서의 객체
    1. 객체 생성
    2. 객체 정의
    Javascript  - prototype(JS객체지향 공부할 때 설명)
                - class(ES6버전 이상일 때 설명)

    JS는 맨땅에 객체를 생성한다.(생성)
    필요한 속성이 있으면 객체에 기능을 붙인다.(정의)
    때문에 동적인 객체라고 함(생성 후 정의)
 */

//객체를 만들었지만 아무런 속성이 없음.
var exam = new Object();

//1. 속성정의 : '.' 이용하여 속성정의(=expand object)
exam.kor = 30; 
exam.eng = 70;
exam.math = 80;

exam.kor = 20;
console.log(exam.kor + exam.eng);

//2. 속성정의 : '[ ]'
exam["jpn"] = 50;
var key = "jpn";

/*
    []내의 값은 문자열. exam.jpn 으로는 꺼낼 수 없다.
    exam의 '속성'을 '변수'를 키로 사용해서 꺼낼 때는
    '.' 방식으로 불가하며 '[]' 방식으로 꺼내야 한다.
    기본적으로 변수를 사용하지 않고 단순히 값을 꺼낼 때는 무조건 '.'를 이용한다.
 */
console.log(exam[key]); //50 정상출력
console.log(exam.key);  //undefined

/*
    변수의 종류(추가 설명 필요)
        var   : 함수범위 변수
        let   : 블록범위 변수
        const : 상수 변수
        
    데이터를 목록화
        선형(=Array)
        맵형(=Map)
            JAVA    : Map형(컬럼명으로 데이터구분)컬렉션, 선형(List형)컬렉션
            자료구조 : Hash형(식별자)
            JS      : Object(=Map형), 선형(=Array))
 */
```
#### 데이터객체와 JSON 생성 방법
```javascript
/*
    Javascript Obejct
    앞서 언급한 것처럼 자바스크립트는 변수를 선언하고 값을 '대입'하는 것이 아니라
    아래와 같이 wrapper class를 선언하여 참조하도록 되어있다.
    하지만 이런 불편한 방식은 사용자에게 매력적이지 않다.
 */
var n = new Boolean(true);
var n = new Number(3);
var s = new String("hello");
var ar = new Array();
var ob = new Object();

//쉽게 표현하고 사용하도록 Javascript Object Notaion(Json)표기법이 적용된다.
var n = true;
var n = 3;

/*
    자바스크립트는 문자열을 표현할 때 "" 보다 ''으로 많이 쓴다.
    html내에 포함되는 언어이기 때문에 문서의 "" 안에 스크립트가 포함될 수 있는데  
    ""가 중첩된다면 충돌이 발새되기 때문이다.
 */
var s = "hello";
var s = 'hello';
var msg = "alert("안녕");"; //충돌

var exam = {}; //Object 선언 다른 방법
exam.kor = 20; //선언 후 초기화 방법-1
var exam = {"kor":30, "eng":40,"math":50}; //선언과 초기화를 동시에 할 수도 있다.
var ar = [3,4,5,6,exam,[7,8,9]]; //배열도 json 표기법
console.log(ar[5][1]); //배열 내 배열 출력
console.log(ar[4].math); //배열 내 객체 출력
```
#### 데이터를 구분하기 위한 표현법
- xml     : 태그형식
- csv     : 콤마 구분법
- json    : 아래 설명

#### Json의 중첩표현
```javascript
//json은 중첩된 데이터의 구조도 쉽게 표현 가능
var notices = [{"id":1, "title":"hello1"},
                {"id":2, "title":"hello2"},
                {"id":3, "title":"hello3"}];
//두번째 객체 데이터 호출 EZ
console.log(notices[1].title);

//이슈상황 : 외부에서 넘겨받은 Json은 문자열로 감싸진다.
var noticetest = '{"id":3, "title":"hello3"}';

//문자열이기 때문에 데이터 호출이 되지 않는다.
console.log(noticetest.title);

/*
    eval() 함수 : 문자열로 표현된 JS코드를 실행하는 함수
    *가급적 사용을 지양한다.(참조-참고사항 : eval은 evil)
 */
eval('var x = 30');
console.log('x : '+x); //30

var notices1 = '[\
                    {"id":1, "title":"hello1"},\
                    {"id":2, "title":"hello2"},\
                    {"id":3, "title":"hello3"}\
                ]';
eval("var ar_noti = "+notices1+";");
console.log(ar_noti[1].id);

/*
    json parser
        eval은 자바스크립트의 코드를 실행해주는 역할일 뿐
        json의 데이터를 파싱해주는 함수는 아니다. 
        json 데이터객체로 바꿔주는 json parser가 있다.
        json.parse를 사용할 때는 반드시 속성명을 문자열("")로 감싸야한다
    
    json 표기법++ 
        속성명을 문자열 표현하거나 or 하지 않아도 된다.
        하지만 유효하지 않은 속성명인 경우 문자열로 표현한다.
        {"id":1, "title-2":"hello"}
 */
var data = JSON.parse('{"id":1, "title":"hello1"}');
console.log(data);

//반대로 json을 문자로 바꿔야할 때도 있다.
var data2 = {id:2, title:"hello2"};

var json = JSON.stringify(data2);
console.log(json);
```

### 참고사항
- [eval은 evil](https://velog.io/@modolee/javascript-eval-is-evil)