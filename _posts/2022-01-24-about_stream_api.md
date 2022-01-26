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
<br>

## 🧪 중개연산

Strean API에 의해 생성된 Stream은 중개 연산을 통해 또 다른 Stream으로 변환될 수 있습니다.
중개 연산은 Stream을 전달받아 Stream을 반환하므로 연속으로 연결해서 사용할 수 있습니다.
또한, Strean의 중개 연산은 필터-맵(filter-map) 기반의 API를 사용함으로 지연(lazy) 연산을 통해 성능을 최적화할 수 있습니다.

Stream API에서 사용할 수 있는 대표적인 중개 연산과 그에 따른 메소드는 다음과 같습니다.

### 필터링

|Method|Desc|
|------|----|
|Stream.filter(조건)|Stream에서 주어진 조건에 맞는 요소만으로 구성된 새로운 Stream을 반환|
|Stream.distinct()|Stream에서 중복된 요소가 제거된 새로운 Stream을 반환|

### 변환

|Method|Desc|
|------|----|
|Stream.map(Functoin())|Stream의 요소들을 주어진 함수에 인수로 전달하여, 그 함수의 결과값으로 이루어진 새로운 Stream을 반환|
|Stream.flatMap(Functoin())|Stream의 요소가 배열이라면, flatMap() 메소드를 사용하여 각 배열의 각 요소의 반환값을 하나로 합친 새로운 Stream을 반환할 수 있음|

### 제한

|Method|Desc|
|------|----|
|Stream.limit()|Stream의 첫 번째 요소부터 전달된 개수만큼의 요소만으로 이루어진 새로운 Stream을 반환|
|Stream.skip()|Stream의 첫 번째 요소부터 전달된 개수만큼의 요소를 제외한 나머지 요소만으로 이루어진 새로운 Stream을 반환|

### 정렬

|Method|Desc|
|------|----|
|Stream.sorted(Comparator)|Stream을 주어진 Comparator를 이용하여 정렬, Comparator를 전달하지 않으면 기본적으로 사전 순으로 정렬|

### 연산 결과 확인

|Method|Desc|
|------|----|
|Stream.peek(Function())|결과 Stream으로부터 요소를 소모하여 추가로 명시된 동작을 수행. 원본 Stream의 요소를 소모하지 않으므로, 주로 연산과 연산 사이에 결과를 확인하며 디버깅이 필요할때 사용|



📌 참고<br>
<http://tcpschool.com/java/java_stream_concept>{: target="_blank"}<br>
<http://tcpschool.com/java/java_stream_creation>{: target="_blank"}<br>

