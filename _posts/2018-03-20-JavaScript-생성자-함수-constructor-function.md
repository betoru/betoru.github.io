---
layout: post
date: 2018-03-20 17:19:12 +0900
title: 'JavaScript: 생성자 함수 constructor function'
category:
  - script language
tags:
  - script language
  - ecmascript
  - javascript
  - constructor
  - function
  - todo
img: js-1.png # Add image post (optional)  
---

* Kramdown table of contents
{:toc .toc}

#### 참고한 글
- [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions)
- [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/constructor](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/constructor)
- [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/new](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/new)
- [http://tobyho.com/2010/11/22/javascript-constructors-and/](http://tobyho.com/2010/11/22/javascript-constructors-and/)

![](/images/prototype-constructor-1.png)

## 생성자 함수가 일반 함수로 호출되는것을 방지하는 방법
```js
function Person(name){
  if (!(this instanceof Person)) {
    return new Person(name);
  }
  this.name = name;
}

var bob = new Person('bob');
var bob2 = Person('bob');
bob instanceof Person; // true
bob2 instanceof Person; // true
```
`new Object()`와 `Object()`의 결과가 같은 이유는 Object 함수가 위처럼 되어 있기 때문이다. 생성자 함수가 new 키워드 없이 일반 함수로써 호출되면 `this`는 생성자 함수의 프로토타입이 아니라 함수를 소유하고있는 객체가 된다. (실행기가 브라우저라면 `this`는 Window다.)

## 생성자'의' 메서드
```js
function Person(name){
  this.name = name;
  this.sayHi = function() {
    return 'Hi, I am ' + this.name;
  }
}
```
위의 코드는 다음처럼 작성하는게 좋다:
```js
function Person(name) {
  this.name = name;
}
Person.prototype.sayHi = function() {
  return 'Hi, I am ' + this.name;
};
```
왜냐하면 첫 번째 코드는 생성되는 인스턴스 개수만큼 `sayHi()` 메서드가 생성되지만 두 번째 코드는 프로토타입의 메서드로 딱 한 번만 생성되고 Person의 인스턴스들은 이 프로토타입의 메서드를 공유하기 때문이다. 즉, 불필요한 함수 생성으로 메모리가 낭비되는걸 방지 할 수 있다.

## 생성자 메서드
생성자 메서드([constructor method](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes/constructor))는 ES2015(ES6)에 추가된 class 구문 내에서 사용한다. **생성자 함수가 아니다.**
```js
class Square extends Polygon {
  constructor(length) {
    // Here, it calls the parent class' constructor with lengths
    // provided for the Polygon's width and height
    super(length, length);
    // Note: In derived classes, super() must be called before you
    // can use 'this'. Leaving this out will cause a reference error.
    this.name = 'Square';
  }

  get area() {
    return this.height * this.width;
  }

  set area(value) {
    this.area = value;
  }
}
```
