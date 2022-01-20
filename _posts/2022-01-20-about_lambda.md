---
title: '[JAVA] 람다 소개!' 
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

// 람다 방식
() -> "Hello World!";
```

또한 람다식 표현은 익명클래스와 동일한 특성을 가지고 있어 람다식이 익명클래스와 같다고도 볼 수 있습니다.
> **익명클래스..?!**<br>
> 생성과 동시에 단 하나의 객체만을 생성하는 클래스로 **일급객체**라는 특징을 지님<br><br>
> **일급객체..?!**<br>
> 다른 객체들에 적용 가능한 연산을 모두 지원하는 개체로 일급객체는 변수로 전달이 가능하고 결과값으로 반환도 가능

``` java
// 기존 방식의 익명클래스 생성
new Object() {
    int min(int x, int y) {
        return x < y ? x : y;
    }
}

// 람다 방식
(x, y) -> x < y ? x : y;
```

## 람다식 표현 작성
1. 람다식 표현은 (매개변수) -> (함수몸체)로 작성합니다.
2. 변수의 Type이 추론 가능한 경우는 Type을 생략할 수 있습니다.
3. 단, Type이 선언된 변수와 선언이 생략된 변수는 서로 연산이 불가능합니다.
4. 함수몸체가 단일 실행문이면 괄호{}를 생략 할 수 있습니다. 
5. 함수몸체가 return문으로만 구성되어 있는 경우 괄호{}를 생략 할 수 없습니다.

``` java
// 정상적으로 동작하는 표현 예제
() -> {}
() -> "hi"
() -> { return "hi"; }

(int x) -> x
(x) -> x
x -> x
(int x) -> { return x; }
x -> { return x; }

(int x, int y) -> x+y
(x, y) -> x+y
(x, y) -> { return x+y; }

(Object obj) -> { obj.method(); }
obj -> { obj.method(); }

// 정상적으로 동작하지 않는 표현 예제
(x, int y) -> x+y   // 에러
```
## ➕장점
- 코드가 간결해집니다.
- 지연 연산을 통해 효율성의 상승(메모리상의 효율성, 불필요한 연산 배체 등)을 기대할 수 있습니다.

> **지연 연산..?!**<br>
> Streaming, 혹은 언어에 따라 체인이라고도 불리는 방식

## ➖단점
- 원소를 FULL SCAN해야하는 경우는 람다식 표현이 기존 표현보다 조금 느릴 수 있습니다.
- 람다식을 남용할 경우 오히려 코드의 이해가 어려워질 수 있습니다.
<br>

## 함수형 인터페이스
람다식 표현을 사용할 때는 이를 저장하기 위한 참조 변수의 타입을 결정해야만 합니다.
```
참조변수의타입 참조변수의이름 = 람다식 표현
```
위의 문법처럼 람다식 표현을 하나의 변수에 대입할 때 사용하는 참조 변수의 타입을 **함수형 인터페이스**라고 부릅니다.<br>

함수형 인터페이스는 추상 클래스와는 달리 **단 하나의 추상 메소드만을 가져야 합니다.**
함수형 인터페이스는 아래와 같이 **@FunctionalInterface** 어노테이션을 통해 명시할 수 있습니다.

``` java
@FunctionalInterface
interface Calc { // 함수형 인터페이스의 선언
    public int getSum(int x, int y);       // 단 하나의 추상 메소드만 선언
}

public class Lambda {
    public static void main(String[] args){
        Calc getSum = (x, y) -> x + y; // 추상 메소드의 구현
        int sum = getSum.sum(1, 2);
    }
}
```
JAVA는 java.util.function 패키지를 통해 함수형 인터페이스를 구현하여 제공합니다.<br>
java.util.function 패키지에 대한 자세한 내용은 [Package.java.util.function](https://docs.oracle.com/javase/8/docs/api/java/util/function/package-summary.html{: target="_blank"})에서 확인바랍니다.<br>

📌 참고<br>
<http://tcpschool.com/java/java_lambda_concept>{: target="_blank"}<br>
