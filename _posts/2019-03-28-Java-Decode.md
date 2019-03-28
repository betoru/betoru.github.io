---
layout: post
date: 2019-03-28 15:47:00 +0900
title: 'Java: Decode'
category:
  - java
tags:
  - java
  - decode
img: java.png # Add image post (optional)
---

* Kramdown table of contents
{:toc .toc}

## Decode란?

`Decode`란 *오라클에서만* 지원하는 함수로써 `SELECT`문 내에 비교연산을 수행해주는 함수이다.
`DECODE`내 선언된 인자의 수에 따라 사용 방식이 다르다.

함수의 사용 방식은 아래와 같다.
```sql
//인자의 수가 3개인 경우

인자 순서에 따라 A, B, C, ... Z 로 정하고 그 값을 나타냈다.
SELECT DECODE(1,2,3) FROM DUAL

```

호출하는 측에선 인자를 생략하거나, 타입이 일치하는(여기선 int) 쉼표로 구분되는 하나 이상의 인자를 전달하며 호출할 수 있다. 인자를 생략할 경우 가변인자의 길이는 0이 되니 주의할 것.

```java
public void showArgs(int... args) {
    for (int i = 0; i < args.length; i++) {
        // 전달받은 인수의 개수만큼 배열의 길이가 결정되므로 그 만큼만 반복
        System.out.println(args[i]);
    }
}
```

향상된 포문을 활용할 경우 다음과 같다:

```java
public void showArgs(int... args) {
    for (int ns : args) {
        System.out.println(ns);
    }
}
```

## example 1

```java
class Args {
    public int multiply(int... args) {
        int result=1;
        for(int ns : args) {
            result = result * ns;
        }
        return result;
    }
}


Args a = new Args();
System.out.println(a.multiply(2, 2, 2, 2));
→ 16
```

## example 2

```java
public static void main(String[] args) {
    m1(1, 2, 3); // 6
    m1(new int[] { 1, 2, 3, 4 }); // 10
}

public static int m1(int... args) {
    int sum = 0;
    for (int i = 0; i < args.length; i++) {
        sum += args[i];
    }
    return sum;
}
```

## main 메서드의 arguments

```java
public static void main(String[] args) { ... }
```

콘솔에서 값을 입력받아 main 메서드에 매게변수로 전달할 때 사용된다.

다음과 같은 클래스가 있을 때:

```java
public class MainTest {
    public static void main(String[] args) {
        System.out.println("args.length : " + args.length);

        if (args.length <= 0) {
            System.out.println("Incorrect usage");
            System.exit(0);
        }

        for (int i = 0; i < args.length; i++) {
            System.out.println("args[" + i + "] = \""+ args[i] + "\"");
        }        
    }
}
```

터미널에서 직접 실행해보면:

```bash
javac MainTest.java

java MainTest
Incorrect usage

java MainTest a 1 b c 3 4 d f
args length : 8
args[0] = "a"
args[1] = "1"
args[2] = "b"
args[3] = "c"
args[4] = "3"
args[5] = "4"
args[6] = "d"
args[7] = "f"
```

요렇게 된다.

끗.
