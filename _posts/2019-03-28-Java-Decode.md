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

>`풀다`라는 단어의 뜻을 가졌으며 *오라클에서만* 지원하는 함수로써 `SELECT`문 내에 비교연산을 수행해주는 함수이다.
`DECODE`내 선언된 인자의 수에 따라 사용 방식이 다르다.

Decode는 선언한 인자의 개수에 따라 사용방식이 달라진다.
인자 개수에 따른 사용 방식은 아래와 같다.
```sql
/*
  인자 수 : 3개(A,B,C)
  A와 B가 같다면 결과는 C
  A와 B가 다르면 결과는 null
*/
SELECT DECODE(A,B,C) FROM DUAL;
```

```sql
/*
  인자 수 : 4개(A,B,C,D)
  A와 B가 같다면 결과는 C
  A와 B가 다르면 결과는 D
*/
SELECT DECODE(A,B,C,D) FROM DUAL;
```

```sql
/*
  인자 수 : 5개(A,B,C,D,E)
  5개부터 인자비교가 달라짐 A-B, A-D
  A와 B가 같다면 결과는 C
  A와 D가 같다면 결과는 E
  둘다 아니면 null
*/
SELECT DECODE(A,B,C,D,E) FROM DUAL;
```

```sql
/*
  인자 수 : 6개(A,B,C,D,E,F)
  5개부터 인자비교가 달라짐 A-B, A-D
  A와 B가 같다면 결과는 C
  A와 D가 같다면 결과는 E
  둘다 아니면 F
*/
SELECT DECODE(A,B,C,D,E,F) FROM DUAL;
```

헷갈릴 수 있는 `Decode` 억지로 외우지말고 자주 써먹어보자.
