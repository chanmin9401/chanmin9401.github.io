---
title: '[JAVA] 디자인 패턴' 
excerpt: "자주 쓰이는 디자인 패턴 소개"
categories:
    - JAVA
tag:
    - JAVA
    - 실무활용
    - 면접대비

author_profile: true    #작성자 프로필 출력 여부

last_modified_at: 2022-02-26 T19:00:00+09:00

toc: true   #Table Of Contents 목차 

toc_sticky: true
---

## 📑 디자인 패턴?
객체지향 프로그램이 복잡해지면서 이를 간결하게 정리할 필요성이 생긴 관계로 '디자인 패턴'이라는 것이 생겼습니다. 디자인 패턴은 프로그래밍 형식을 정하는 일종의 약속이며, 객체지향 프로그래밍 설계를 할 때 발생될 수 있는 문제들을 피하기 위해 사용됩니다.

또한 의사소통의 수단으로 활용될 수도 있습니다. 예를 들어 새로운 서비스를 만들어야할 때, 장황한 설명대신 "Facade 패턴으로 가시죠" 라고 하면 이 패턴을 알고 있는 사람들은 금방 의도를 파악할 수 있습니다.

## 🛒디자인 패턴의 종류
### 생성 패턴(추상 객체 인스턴스화)
#### 1. Factory Method
상위 클래스와 하위 클래스가 있을 때, 팩토리 클래스를 두어 하위 클래스의 인스턴스를 생성하는 패턴입니다.

```java
public class Car {
    Car(){
    }
}
=====================================
public class HyundaiCar extends Car{
    HyundaiCar(){
    }
}
=====================================
public class KiaCar extends Car{
    KiaCar(){
    }
}
```
위 와 같이 Car 클래스를 상속한 HyundaiCar와 KiaCar 클래스가 있다면, 자동차와 관련된 클래스를 다루는 로직에서 아래와 같이 작성을 하는 경우가 많습니다.
```java
if(carBrand.equals("Hyundai")){
    return new HyunDaiCar();
}else if(carBrand.equals("kia")){
    return new KiaCar();
}else if(...){
    ...
}
```
그러나 위와 같이 작성을 하는 경우, 원하는 자동차의 생성자를 반환하는 로직뿐만 아니라 이를 위해 어떤 자동차 브랜드인지 분류해야하는 기능까지 같이 지니게 되어 로직이 불필요하게 길어질 수 있습니다. 또한 자동차 브랜드의 종류가 늘어날 경우 위와 비슷한 모든 로직에 브랜드별 분기처리를 추가해야하며 이때 분기처리 로직이 누락된 부분에서는 에러가 발생할 가능성도 생깁니다.

위 와 같은 문제를 브랜드 분류와 Car 객체 생성을 위임할 Factory를 생성하여 개선해볼 수 있습니다.
```java
public class CarFactory {
    static Car create(String brand) {
        if(brand.equals("Hyundai")) {
            return new HyundaiCar();
        } else if(brand.equals("Kia")) {
            return new KiaCar();
        } else if(...){
            ...
        }
        return null;
    }
}
```
CarFactory를 활용한다면 아래와 같이 코드의 길이도 줄일 수 있고, 브랜드 분류라는 로직은 신경쓸 필요가 없어지므로 생산성도 향상될 것으로 기대됩니다.

```java
// 개선 전
if(carBrand.equals("Hyundai")){
    return new HyunDaiCar();
}else if(carBrand.equals("Kia")){
    return new KiaCar();
}else if(...){
    ...
}
// 개선 후
return CarFactory.create(brand);
```

#### 2. Builder 
Builder 패턴은 인스턴스를 생성자를 통해 직접 생성하지 않고, Builder라는 내부 클래스를 통해 간접적으로 생성하게 하는 패턴입니다.

```java
class Car {
 
    String brand;
    String carClass;
 
    private Car(String brand, String carClass) {
        this.brand = brand;
        this.carClass = carClass;
    }
 
    public static class Builder {
        
        String brand=null;
        String carClass=null;
 
        public Builder() {
        }
 
        public Builder setBrand(String brand) {
            this.brand = brand;
            return this;
        }
 
        public Builder setCarClass(String carClass) {
            this.carClass = carClass;
            return this;
        }
 
        public Car build() {
            return new Car(brand, carClass);
        }
    }
}
```
위와 같이 Builder를 생성 후,
```java
Car car = new Car.Builder().setBrand("HyunDai").setCarClass("Grandeur").build();
```
Car 인스턴스를 생성할 수 있습니다.

Builder 패턴을 사용하면 private 등의 접근 제한자로 제한하여 외부에서 임의로 접근하는 것을 막아 클래스와 사용대상의 결합도를 떨어뜨리고, Builder라는 내부 클래스를 통해 해당 클래스를 간접적으로 생성할 수 있습니다. 

또한 인스턴스 생성에 필요한 파라미터가 많은 경우, 각 파라미터가 무엇을 의미하는지 쉽게 파악할 수 있습니다.

#### 3. Singleton
```java
class Singleton {
 
    static final Singleton instance = new Singleton();
 
    private Singleton() {
        //초기화
    } 
    public Singleton getInstance() {
        return instance;
    }
}

```
Singleton은 클래스의 객체를 하나만 만들어야 하는 경우 사용합니다. 클래스 내에서 인스턴스가 단 하나뿐임을 보장하므로, 프로그램 전역에서 해당 클래스의 인스턴스를 바로 얻을 수 있고, 불필요한 메모리 낭비를 최소화할 수 있습니다.

> Eager initialization(사전 초기화)

클래스 로딩시에 인스턴스를 생성하는 방법입니다. 위의 예시가 사전 초기화인데, 멀티스레드 환경에서의 이중 객체 생성 문제가 없지만, 인스턴스를 호출하지 않아도 무조건 클래스를 초기화하기에 메모리 효율이나 연산 효율은 낮습니다.

>Lazy initialization

인스턴스를 실제로 사용할 시점에서 인스턴스를 생성하는 방법입니다. 멀티쓰레드 환경에서 자칫 이중 객체 생성 문제가 발생할 수 있으나, 인스턴스를 실제로 사용하지 않는다면 메모리와 연산량을 아낄 수 있다는 장점이 있습니다.

### 구조 패턴(객체 결합)
#### 1. Facade
Facade는 프랑스어 Façade에서 차용된 단어로 보통 건물의 출입구로 이용되는 정면 외벽 부분을 가리키는 말입니다.

Facade 패턴은 시스템의 복잡성을 감추고, Client가 시스템에 접근할 수 있는 인터페이스를 Client에게 제공합니다. Facade 패턴은 기존의 시스템에 인터페이스를 추가하여 복잡성을 감추기 위해 사용된다.

1단계 : 인터페이스 생성
```java
public interface Car {
    void move();
}
```
2단계 : 구현체 생성
```java
public class HyundaiCar implements Car {
   @Override
   public void move() {
      System.out.println("HyundaiCar::move()");
   }
}
public class KiaCar implements Car {
   @Override
   public void move() {
      System.out.println("KiaCar::move()");
   }
}
```
3단계 : Facade 클래스 생성
```java
public class CarMove {
    private Car HyundaiCar;
    private Car KiaCar;
 
    public CarMove() {
        HyundaiCar = new HyundaiCar();
        KiaCar = new KiaCar();
    }
    public void moveHyundaiCar(){
        HyundaiCar.move();
    }
    public void moveKiaCar(){
        KiaCar.move();
    }
}

```
사용 예시
```java
public class CarMoveFacade {
    public static void main(String[] args) {
        CarMove carMove = new CarMove();
 
        carMove.moveHyundaiCar();
        carMove.moveKiaCar();
    }
}
```
📌 참고<br>
<https://shlee0882.tistory.com/188>{: target="_blank"}<br>
