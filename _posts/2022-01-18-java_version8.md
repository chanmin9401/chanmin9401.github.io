---
title: '[JAVA] JAVA8부터 달라진 점' 
excerpt: "JAVA8관련 기능 소개"
categories:
    - JAVA
tag:
    - JAVA
    - 면접대비

author_profile: true    #작성자 프로필 출력 여부

last_modified_at: 2022-01-19 T19:00:00+09:00

toc: true   #Table Of Contents 목차 

toc_sticky: true
---

## 🙄 JAVA8의 등장!
2014년 **JAVA SE 8**이 새로 발표되며 눈에 띄는 몇가지 기능 및 특징들이 추가되었습니다.<br>
- lambda Expression (이하 람다식 표현)
- Stream API
- java.time package
- Nashorn

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

자세한 내용은 [**람다 소개!**](https://chanmin9401.github.io/java/about_lambda/)에서 다뤄보겠습니다.

## Stream API
기존에는 많은 양의 데이터를 다루기 위해 주로 Collection Framework의 List, Map, Set 인터페이스의 구현체를 사용하였습니다.
이렇게 구현한 객체에 접근하고 가공하여 원하는 결과값을 얻기 위해서는 반복문이나 반복자(iterator)를 사용하는 새로운 코드를 작성해야 합니다.<br>
이러한 이유로 비즈니스 로직의 복잡도와 가독성이 반비례하는 경우가 많습니다.
또한, List, Map, Set 인터페이스의 구현체들은 각각의 형태가 조금씩 상이하기 때문에 정형화된 처리 패턴을 적용하는 것이 어려운 경우가 많습니다.<br>

Stream API는 이러한 문제점을 극복하기 위해서 도입되었습니다.
Stream API는 데이터를 추상화하여 다루므로, 다양한 방식으로 저장된 데이터를 읽고 쓰기 위한 공통된 방법을 제공합니다.
따라서 Stream API를 이용하면 배열이나 Collection뿐만 아니라 파일에 저장된 데이터도 모두 같은 방법으로 다룰 수 있습니다.

String Array의 각 항목을 Stream으로 변환하여 출력하는 방식은 다음과 같습니다.
``` java
String[] arr = new String[]{"넷", "둘", "셋", "하나"};

// 기존 배열 출력 방식
for(int i = 0; i<arr.length; i++){
    System.out.print(arr[i] + " ");
}

// Stream 변환 후 출력 방식
Stream<String> stream1 = Arrays.stream(arr);
stream1.forEach(e -> System.out.print(e + " "));
```

자세한 내용은 [**Stream API 소개!**](https://chanmin9401.github.io/java/about_stream/)에서 다뤄보겠습니다.

## java.time 패키지
기존에 사용된 Date, Calendar 패키지는 아래와 같은 단점 및 문제점들이 있습니다.
1. Calendar 인스턴스는 불변 객체가 아니라서 값이 수정될 수 있음.
2. 윤초와 같은 특수 케이스는 개별구현이 필요.
3. Calendar 클래스에서는 월을 나타낼 때 1월부터 12월을 0부터 11까지로 표현해야함. <br>
그러나 요일을 표시할 때는 1부터 7까지로 표현하는 등 일관적이지 못함.

그래서 많은 자바 개발자들은 Calendar 클래스뿐만 아니라 더 나은 성능의 **Joda-Time**이라는 라이브러리를 함께 사용해왔고,
JAVA SE 8 버전부터 Joda-Time 라이브러리를 발전시킨 새로운 날짜와 시간 API인 java.time 패키지를 제공하기 시작하였습니다.

자세한 내용은 [**Time패키지 활용법!**](https://chanmin9401.github.io/java/about_time_package/)에서 다뤄보겠습니다.

## Nashorn
JAVA SE 8 버전 이전까지는 자바스크립트의 기본 엔진으로 Rhino가 사용되어 왔습니다.
그러나 자바의 최신 개선 사항 등을 제대로 활용하지 못하는 등의 문제로 JAVA SE 8 버전부터 자바스크립트의 새로운 엔진으로 오라클의 Nashorn을 도입하게 됩니다.
Nashorn은  Rhino에 비해 성능과 메모리 관리 면에서 크게 개선된 스크립트 엔진입니다.<br>

JAVA 11 기준으로는
> "ECMA 스펙 변경마다 이를 관리하기가 어렵다"
는 이유로 Nashorn 엔진을 제거하고 [**GraalVM**](https://www.graalvm.org/){: target="_blank"}으로 대체하고 있습니다.

📌 참고<br>
<http://www.tcpschool.com/java/java_intro_java8>{: target="_blank"}<br>
<https://mangkyu.tistory.com/113>{: target="_blank"}
