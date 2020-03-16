---
layout: post
date: 2020-03-16 16:59:00 +0900
title: 'JavaScript: lazyload'
category:
  - javascript
tags:
  - javascript
  - image
  - lazy
  - lazyload
img: js-1.png # Add image post (optional)  
---

* Kramdown table of contents
{:toc .toc}

## Rank Over VS Row_number Over

> 어떤 SCORE 에 의해 데이터를 정렬해야 할 때 이 두 가지의 함수 중 적절한 함수를 쓰도록 한다.

#### Rank Over()
기준 데이터를 정렬했을 때 동일한 값의 데이터는 동일한 정렬값을 부여하는 함수. 함수명 그대로 `RANK`

```
예
SELECT NUM, NM, RANK () OVER (ORDER BY NUM DESC) RANK
  FROM (SELECT 1 AS NUM, 'a1' NM FROM DUAL
        UNION ALL
        SELECT 2 AS NUM, 'a2' NM FROM DUAL
        UNION ALL
        SELECT 3 AS NUM, 'a3' NM FROM DUAL
        UNION ALL
        SELECT 4 AS NUM, 'a4' NM FROM DUAL
        UNION ALL
        SELECT 4 AS NUM, 'a5' NM FROM DUAL
        UNION ALL
        SELECT 4 AS NUM, 'a6' NM FROM DUAL
        UNION ALL
        SELECT 5 AS NUM, 'a7' NM FROM DUAL)
 WHERE 1 = 1;
```
`결과`

|NUM|NM |RANK|
|:-:|:-:|:-:|
|5  |a7 |	1 |
|4  |a4 |	2 |
|4  |a6 |	2 |
|4  |a5 |	2 |
|3  |a3 |	5 |
|2  |a2 |	6 |
|1  |a1 |	7 |

#### Row_number Over()
기준 데이터를 정렬했을 때 동일한 값의 데이터와 상관없이 기준 데이터값을 정렬하여 순차적으로 정렬값을 부여한 함수
```
SELECT NUM, NM, ROW_NUMBER () OVER (ORDER BY NUM DESC) RANK
  FROM (SELECT 1 AS NUM, 'a1' NM FROM DUAL
        UNION ALL
        SELECT 2 AS NUM, 'a2' NM FROM DUAL
        UNION ALL
        SELECT 3 AS NUM, 'a3' NM FROM DUAL
        UNION ALL
        SELECT 4 AS NUM, 'a4' NM FROM DUAL
        UNION ALL
        SELECT 4 AS NUM, 'a5' NM FROM DUAL
        UNION ALL
        SELECT 4 AS NUM, 'a6' NM FROM DUAL
        UNION ALL
        SELECT 5 AS NUM, 'a7' NM FROM DUAL)
 WHERE 1 = 1;

```
`결과`

|NUM|NM |RANK|
|:-:|:-:|:-:|
|5  |a7 |	1 |
|4  |a4 |	2 |
|4  |a6 |	3 |
|4  |a5 |	4 |
|3  |a3 |	5 |
|2  |a2 |	6 |
|1  |a1 |	7 |
