---
layout: post
date: 2022-05-10 22:13:00 +0900
title: 'Java: Variable&Method'
category:
  - program language
tags:
  - program language
  - java
  - variable
  - method
img: java.png # Add image post (optional)  
---

* Kramdown table of contents
{:toc .toc}

## 변수와 메서드
### 변수
> 변수에는 클래스 변수, 인스턴스 변수, 지역변수 세 종류가 있다.  
> 이런 변수의 종류를 결정짓는 것은 `선언된 위치`이다.  
> 멤버변수를 제외한 나머지 변수는 모두 지역변수이며 멤버변수 중 static이 붙은 것은 클래스, 붙지 않은 것은 인스턴스변수다.

```java
class Variable{
    int instanceVariable;       //인스턴스변수
    static int classVariable;   //클래스변수
    
    void method(){
        int localVariable;      //지역변수
    }
}
```
정리하면 아래와 같다
- 변수의 종류
  - 클래스 변수 : 모든 인스턴스가 공통된 저장공간을 공유함. 그래서 공유 변수라고 부르기도 함.
    - 선언 위치
      - 클래스 영역
    - 생성시기
      - 클래스가 메모리에 올라갈 때
  - 인스턴스 변수 : 클래스의 인스턴스 생성시 만들어지며, 인스턴스 생성 후 변수의 값을 읽고 저장하는 것이 가능. 독립적인 저장공간을 가지므로 서론 다른 값을 가질 수 있다.
    - 선언 위치
      - 클래스 영역
    - 생성시기
      - 인스턴스가 생성되었을 때
  - 지역 변수 : 메서드 내에 선언되어 메서드 내에서만 사용 가능하며 메서드가 종료되면 소멸되어 사용이 불가함.
    - 선언 위치
      - 클래스 영역을 제외한 영역
        - 메서드, 생성자, 초기화 블럭 내부
    - 생성시기
      - 변수 선언문이 수행되었을 때

위의 내용들을 종합하면 아래의 코드로 정리할 수 있다.  
클래스 내 선언된 인스턴스와 클래스 변수(또는 메서드)인 멤버변수는 서로 사용할 수 있으나 static 메서드의 경우 인스턴스 변수(메서드)는 사용할 수 없다. 
```java
public class TestClass2 {
    int iv; //인스턴스변수
    static int cv; //클래스 변수

    void instanceMethod(){      //인스턴스 메서드
        System.out.println(iv); //인스턴스 변수 사용가능
        System.out.println(cv); //클래스변수 사용가능
    }

    static void statiMethod(){  //static 메서드
        System.out.println(iv); //인스턴스 변수 사용 불가
        System.out.println(cv); //클래스 변수 사용 가능
    }
    
}
```