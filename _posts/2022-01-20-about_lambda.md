---
title: '[JAVA] 람다에 대한 고찰...' 
excerpt: "람다 개념 및 활용법 소개"
categories:
    - JAVA
tag:
    - JAVA
    - 면접대비

author_profile: true    #작성자 프로필 출력 여부

last_modified_at: 2022-01-20 T19:00:00+09:00

toc: true   #Table Of Contents 목차 

toc_sticky: true
---

## lambda Expression
람다식 표현은 간단히 말해 메소드를 하나의 식으로 표현한 것입니다.<br>
식별자 없이 실행할 수 있는 함수 표현식을 의미하며, 익명함수라고도 부릅니다.
> **익명함수(anonymous function)?!**<br>
> 익명함수란 함수의 이름이 없는 함수로, 익명함수들은 모두 일급 객체이다.<br>
> 일급 객체인 함수는 변수처럼 사용가능하며 매개 변수로 전달이 가능하는 등의 특징을 가지고 있다.

메소드를 람다식 표현으로 표현하면 클래스와 객체를 생성하지 않아도 메소드를 사용할 수 있습니다.<br>
또한, 람다식 표현으로 작성된 메소드는 다른 메소드의 매개변수로 전달될 수도 있고, 결과값으로 반환될 수도 있습니다.<br>

람다식 표현을 기존 표현방식과 아주 간단하게 비교를 하자면,
``` java
// 기존 방식의 함수 선언
public String hello() { return "Hello World!"; }

// 람다 방식의 함수 선언
() -> "Hello World!";
```
위와 같이 불필요한 코드를 줄여 가독성을 높이는 것이 눈에 띄는 장점입니다.

📌 참고<br>
<http://www.tcpschool.com/java/java_intro_java8>{: target="_blank"}<br>
