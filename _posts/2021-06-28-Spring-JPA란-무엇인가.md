---
layout: post
date: 2021-06-28 11:40:00 +0900
title: 'Spring: JPA란 무엇인가?'
category:
  - spring
tags:
  - springframework
  - jpa
  - hibernate
img: spring.png
---

- JPA란 무엇인가 두둥! 탁!
{:toc .toc}

#### 참고한 글
- 자바 ORM표준 프로그래밍 API, 김영한 저

## JPA 란?
>JPA(Java Persisitence API)는 자바 진영의 ORM 기술 표준을 일컫는다.
과거 자바 진영은 엔터프라이즈 자바 빈즈(EJB)라는 기술 표준을 만들었다. 그 안에는 Entity Bean이란 ORM기술이 있었다.
하지만 너무 복잡하고 기술 성숙도가 낮았으며, 자바 엔터프라이즈(J2EE) 애플리케이션 서버에서만 동작했다. 이때 하이버네이트(Hibernate.org)라는 오픈소스 ORM Framework가 등장했는데 EJB ORM 기술과 비교해 가볍고 실용적이며 기술 성숙도가 높았다. 또한 자바 엔터프라이즈 애플리케이션 서버없이 동작이 가능했는데 이 때문에 많은 개발자가 사용하게 됐다. 결국 EJB 3.0에서 하이버네이트를 기반으로 새로운 자바 ORM 기술 표준이 만들어졌는데 이것이 바로 JPA다. 

![](/images/jpa/jpa_interface.png)

*자바 어플리케이션과 JDBC API 사이에서 동작*
![](/images/jpa/jpa_is.png)

## ORM(Object Relational Mapping)
>객체와 테이블을 매핑해서 패러다임의 불일치를 개발자 대신 해결해준다.

## **객체**를 저장하는 코드는 심플하게
```java
jpa.persist(member); // 간단하지?
```

![](/images/jpa/jpa_save.png)

## **객체**를 조회하는 코드는 영문장을 떠올려봐
```java
Member member = jpa.find(memberId); // 멤버 아이디로 관련된 데이터 찾아 member 객체에 담는다.
```

![](/images/jpa/jpa_search.png)

## 왜! JPA를 사용해야 하죠?
### 생산성
- JPA를 자바 컬렉션에 객체를 저장하듯 JPA에게 저장할 객체를 전달.
- INSERT SQL을 작성하고 JDBC API 사용하는 지루하고 반복적인 일을 JPA가 대신 처리해준다.(Insert SQL = SQL Statement를 대신 작성의미?)
- CREATE TABLE같은 DDL문 자동 생성
- 기존 데이터베이스 설계 중심의 패러다임에셔 객체 설계 중심으로 역전
```java
jpa.persist(member);    // 저장
Member member = jpa.find(memberId);     // 조회
```

### 유지보수
```text
기존에 엔티티에 필드 추가시 등록, 수정, 조회 관련 코드 모두 변경했음.
JPA를 사용 시 위의 과정을 JPA가 대신 처리.
개발자가 작성해야 할 SQL과 JDBC API 코드를 JPA가 대신 처리해줌으로 유지보수해야 하는 코드 수가 줄어든다.
```

### 패러다임 불일치 해결
- 상속, 연관관계, 객체 그래프 탐색, 비교하기 같은 패러다임 불일치 해결

### 성능
- 다양한 성능 최적화 기회 제공
- 어플리케이션과 데이터베이스 사이에 존재함으로 여러 최적화 시도 가능

### 데이터 접근 추상화와 벤더 독립성
- 데이터베이스 기술에 종속되지 않도록 한다.
- 데이타베이스를 변경하면 JPA에게 다른 데이터베이스를 사용한다고 알려주면 됨.

![](/images/jpa/jpa_vendor_indifendent.png)
