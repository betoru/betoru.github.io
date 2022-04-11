---
layout: post
date: 2022-04-10 22:17:00 +0900
title: 'JavaScript: VanillaJs-DOM-#2-Basic'
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

### 데이터
#### 연산자
```javascript
        var x = 3;
        var y = 3;
        
        // '==' x,y 변수가 참조하는 값의 비교
        // '===' x, y가 참조하는 박스(주소)의 비교
        document.write(x == y); //true
        document.write(x === y);//true
        
        //의외로 값과 주소의 비교결과가 모두 true, 주소는 다를 것이라 예상했음.
        //그렇다면 다른 박스(주소)에 담고싶을 때는?
        var y = new Number(3);
        document.write(x == y); //true 
        document.write(x === y);//false

        //다른 형에 대한 연산
        // '-' 연산자 : 숫자, 문자 => 숫자연산 = 1
        // - 연산자는 숫자로 변환
        document.write(3-"2");
        document.write("<br />");
        document.write("3"-2);
        document.write("<br />");
        document.write("3"-"2");
        document.write("<br />");
        
        // '+' 연산자 : 숫자, 문자 => 문자연산 = 32
        // + 연산자는 문자로 변환
        document.write(3+"2");
        document.write("<br />");
        document.write("3"+2);
        document.write("<br />");
        document.write("3"+"2");
```

#### 반복문
##### foreach
>arr.forEach(callback(currentvalue[, index[, array]])[, thisArg])  
`callback`  
각 요소에 대해 실행할 함수. 다음 세 가지 매개변수를 받습니다.  
`currentValue`  
처리할 현재 요소.  
`index Optional`  
처리할 현재 요소의 인덱스.  
`array Optional`  
forEach()를 호출한 배열.  
`thisArg Optional`  
callback을 실행할 때 this로 사용할 값.
```javascript

        //배열 데이터의 일반적인 반복문
        var ar = ["hello","hi","greeting","bye"];
        for(var i=0; i<ar.length; i++){
            document.write(ar[i]+", ");
        }

        document.write("<br />");
        document.write("<br />");
        document.write("foreach just start <br />");
        ar.forEach(function(el){
            document.write(el+", ");
        });
        //결과 : hello, hi, greeting, bye,

        document.write("<br />");
        document.write("<br />");
        document.write("foreach func start <br />");
        ar.forEach(function(el, i, arr){
            document.write("el : "+el+", ");
            document.write("<br />");
            document.write("index : "+i+", ");
            document.write("<br />");
            document.write("arr : "+arr+", ");
            document.write("<br />");
            document.write("<br />");
        });

        document.write("<br />");
        document.write("<br />");
        document.write("foreach lamda start <br />");
        ar.forEach((el,i,arr) => {
            document.write("el : "+el+", ");
            document.write("<br />");
            document.write("index : "+i+", ");
            document.write("<br />");
            document.write("arr : "+arr+", ");
            document.write("<br />");
            document.write("<br />");
        });
        /**
         * 결과
         * el : hi,
         *index : 1,
         *arr : hello,hi,greeting,bye,
         * 
         *el : greeting,
         *index : 2,
         *arr : hello,hi,greeting,bye,
         * 
         *el : bye,
         *index : 3,
         *arr : hello,hi,greeting,bye,
         */

        var list = ['a', 'b', 'c'];
        var test = function(el,i,arr){console.log(el+this.arg)};
        list.forEach(test,{arg:10});
        > "a10"
        > "b10"
        > "c10"

```
##### for-in
```javascript
        /**
         * for-in
         *  위의 foreach는 값을 바로 매핑해줘 그냥 쓰면됐다.
         *  for-in은 왜 인덱스를 할당하는거지 귀찮게?
         *  배열일 때는 값을 매핑해주면 사용하기 편하나 object처럼 key:value 형태는 값을 꺼내기가 까다롭다.
         *  for-in을 사용하면 index 또는 key 형태를 가져올 수 있기에 활용할 수 있다.
         */
        var ob = {id:1,title:"hello",writeId:"newlec"};
        for (const i in ob) {
            document.write(i+" : "+ob[i]+", "); //결과 : id : 1, title : hello, writeId : newlec 
            document.write("<br/ >");
        }
```