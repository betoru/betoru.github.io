---
layout: post
date: 2021-06-23 16:40:00 +0900
title: 'Spring: YAML VS PROPERTIES'
category:
  - framework
tags:
  - framework
  - spring
  - springboot
  - java
  - yml
  - properties
img: spring.png # Add image post (optional)
---

* YAML VS PROPERTIES
{:toc .toc}

## YAML

YAML은 XML, C, 파이썬, 펄, RFC2822에서 정의된 e-mail 양식에서 개념을 얻어 만들어진 '사람이 쉽게 읽을 수 있는' 데이터 직렬화 양식이다. 2001년에 클라크 에반스가 고안했고, Ingy dot Net 및 Oren Ben-Kiki와 함께 디자인했다.

YAML이라는 이름은 "YAML은 마크업 언어가 아니다 (YAML Ain't Markup Language)” 라는 재귀적인 이름에서 유래되었다. 원래 YAML의 뜻은 “또 다른 마크업 언어 (Yet Another Markup Language)”였으나, YAML의 핵심은 문서 마크업이 아닌 데이터 중심에 있다는 것을 보여주기 위해 이름을 바꾸었다. 오늘날 XML과 JSON이 데이터 직렬화에 주로 쓰이기 시작하면서, 많은 사람들이 YAML을 '가벼운 마크업 언어'로 사용하려 하고 있다.

## PROPERTIES

properties는 응용 프로그램의 구성 가능한 파라미터들을 저장하기 위해 자바 관련 기술을 주로 사용하는 파일들을 위한 파일 확장자이다. 국제화와 지역화를 위한 문자열들을 저장하는데 사용할 수도 있는데 이것을 Property Resource Bundles로 부른다.

각 파라미터는 문자열들의 일부로 저장되는데, 한 문자열은 파라미터의 이름(키)을 저장하며, 다른 하나는 값을 저장한다.
properties의 각 줄은 일반적으로 하나의 프로퍼티를 저장한다. 키=값, 키 = 값, 키:값, 키 값과 같이 여러 형태가 올 수 있다.

## 각 표현 방식의 차이
```yml
#YAML
server :
  port : 8002
spring :
  mvc :
    view :
      prefix : /WEB-INF/view/
      suffix : .jsp
```      

```properties
#PROPERTIES
server.port=8002
spring.mvc.view.prefix=/WEB-INF/view/
spring.mvc.view.suffix=.jsp
```
