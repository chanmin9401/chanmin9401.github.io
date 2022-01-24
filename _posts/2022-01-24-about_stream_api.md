---
title: '[JAVA] Stream API 소개!' 
excerpt: "Stream API 개념 및 활용법 소개"
categories:
    - JAVA
tag:
    - JAVA
    - 면접대비

author_profile: true    #작성자 프로필 출력 여부

last_modified_at: 2022-01-24 T19:00:00+09:00

toc: true   #Table Of Contents 목차 

toc_sticky: true
---

## 💻 Stream API!
Stream API는 데이터를 추상화하여 다루고 다양한 방식으로 저장된 데이터를 읽고 쓰기 위한 공통된 방법을 제공합니다.
Collection뿐만 아니라 파일에 들어있는 데이터도 Stream객체로 변환하면 동일한 방법으로 처리할 수 있습니다.

## 🎈 Stream의 특징
1. Stream은 외부 반복을 통해 작업하는 컬렉션과는 달리 내부 반복을 통해 작업을 수행합니다.
2. Stream은 원본 데이터를 변경하지 않지만, Collection과는 달리 재사용이 불가능합니다.
3. Stream연산은 Filter-Map 기반의 API를 사용하여 Lazy연산을 통해 성능을 최적화합니다.
4. Stream은 parallelStream() 메소드를 통한 손쉬운 병렬 처리를 지원합니다. 

## 🌊 Stream API 연산 과정
1. Stream 생성
2. 중개연산
3. 최종연산

<p align="center">
    <img src="https://user-images.githubusercontent.com/26996562/150715979-0f9dce8b-689c-4fac-a769-8baad3def0a8.png" alt="about_stream_api_img_1"/>
</p>

## 🛒 Stream 생성
Stream API는 다양한 데이터 소스에서 생성할 수 있습니다.
- Collection
- Arrays
- Variable Parameters
- Range Value
- Random Value
- Lambda Expression
- File

``` java
// From Collection
ArrayList<Integer> list = new ArrayList<Integer>();
list.add(4);
list.add(2);
list.add(3);
list.add(1);

Stream<Integer> stream = list.stream();

// From Arrays
String[] arr = new String[]{"A", "B", "C", "D"};

Stream<String> stream1 = Arrays.stream(arr);
Stream<String> stream2 = Arrays.stream(arr, 1, 3); // 특정 범위로 생성 가능

// From Variable Parameters
Stream<Double> stream = Stream.of(1.0, 2.5, 3.8, 5.9);

// From Range Value
IntStream stream1 = IntStream.range(1, 4);          // result : 1,2,3
IntStream stream2 = IntStream.rangeClosed(1, 4);    // result : 1,2,3,4

// From Random Value
IntStream stream = new Random().ints(4);
LongStream stream = new Random().longs(4);
DoubleStream stream = new Random().doubles(4);
// 난수 생성 시 parameter를 전달받지 않는다면 무한한 사이즈의 스트림이 생성되므로, 
// limit()을 사용하여 크기 제한을 두어야함
Stream<Double> randoms = Stream.generate(Math::random).limit(5);

// With Lambda Expression
IntStream stream = Stream.iterate(2, n -> n + 2); // 2, 4, 6, 8, 10, ...

// From File
String<String> stream = Files.lines(Path path);
```

📌 참고<br>
<http://tcpschool.com/java/java_stream_concept>{: target="_blank"}<br>
<http://tcpschool.com/java/java_stream_creation>{: target="_blank"}<br>

