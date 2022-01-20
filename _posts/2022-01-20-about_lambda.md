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

## 💻 lambda Expression
람다식, 또는 람다 함수는 프로그래밍 언어에서 사용되는 개념으로 익명 함수를 지칭하는 용어입니다.
람다식 표현은 JAVA에 종속되는 것이 아니라 Scala, C++, C#, GO, Javascript, Python 등 다양한 언어에서 활용되는 표현방식의 일종이라고 이해하면 될거 같습니다. (개인적인 소견...)<br>

실무에서는 **코드의 간결함, 지연 연산을 통한 퍼포먼스 향상** 과 같은 특징으로 인해 비교적 중요하게 다루어지고 있습니다.
<br><br>
아래와 같이 메소드를 람다 표현식으로 표현하면, 클래스를 작성하고 객체를 생성하지 않아도 메소드를 사용할 수 있습니다.
``` java
// 기존 방식의 함수 선언
public String hello() { return "Hello World!"; }

// 람다 방식의 함수 선언
() -> "Hello World!";
```
또한 람다식 표현은 익명클래스와 동일한 특성을 가지고 있어 람다식이 익명클래스와 같다고도 볼 수 있습니다.
> **익명클래스..?!**<br>
> JAVA에서 클래스의 생성과 동시에 단 하나의 객체만을 생성하는 클래스
``` java
// 기존 방식의 함수 선언
new Object() {
    int min(int x, int y) {
        return x < y ? x : y;
    }
}

// 람다 방식의 함수 선언
(x, y) -> x < y ? x : y;
```

## ➕장점
- 코드가 간결해집니다.
- 지연 연산을 통해 퍼포먼스 효율성 상승(메모리상의 효율성, 불필요한 연산 배체 등)을 기대할 수 있습니다.

> **지연 연산..?!**<br>
> Streaming, 혹은 언어에 따라 체인이라고도 불리는 방식

## ➖단점
- 원소를 FULL SCAN해야하는 경우는 람다식 표현이 기존 표현보다 조금 느릴 수 있습니다.
- 람다식을 남용할 경우 오히려 코드의 이해가 어려워질 수 있습니다.
<br>


📌 참고<br>
<http://www.tcpschool.com/java/java_intro_java8>{: target="_blank"}<br>
