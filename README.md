# Chanmin's GitHub Blog

### 검색

|Method|Desc|
|------|----|
|Stream.findFirst()<br>Stream.findAny()|Stream에서 첫 번째 요소를 참조하는 Optional 객체를 반환|

일반적으로 findFirst()와 findAny()는 같은 결과를 출력합니다.
하지만 병렬 Stream인 경우에는 findAny() 메소드를 사용해야만 정확한 연산 결과를 반환할 수 있습니다.

### 검사

|Method|Desc|
|------|----|
|Stream.anyMatch()|Stream의 일부 요소가 특정 조건을 만족할 경우 true를 반환|
|Stream.allMatch()|Stream의 모든 요소가 특정 조건을 만족할 경우 true를 반환|
|Stream.noneMatch()|Stream의 모든 요소가 특정 조건을 만족하지 않을 경우 true를 반환|

### 통계

|Method|Desc|
|------|----|
|Stream.count()|Stream 요소의 총 개수를 long 타입의 값으로 반환|
|Stream.max()<br>Stream.min()|Stream의 요소 중에서 가장 큰 값과 가장 작은 값을 가지는 요소를 참조하는 Optional 객체 반환|

### 수집

|Method|Desc|
|------|----|
|Stream.collect(Collectors)|인수로 전달되는 Collectors 객체에 구현된 방법대로 Stream의 요소를 수집|

Collectors 클래스에는 미리 정의된 다양한 방법이 클래스 메소드로 정의되어 있습니다.
이 외에도 사용자가 직접 Collector 인터페이스를 구현하여 자신만의 수집 방법을 정의할 수도 있습니다.

Stream 요소의 수집 용도별 사용할 수 있는 Collectors 메소드는 다음과 같습니다.

1. 배열이나 컬렉션으로 변환 : toArray(), toCollection(), toList(), toSet(), toMap()
2. 요소의 통계와 연산 메소드와 같은 동작을 수행 : counting(), maxBy(), minBy(), summingInt(), averagingInt() 등
3. 요소의 소모와 같은 동작을 수행 : reducing(), joining()
4. 요소의 그룹화와 분할 : groupingBy(), partitioningBy()

Collectors에 대한 자세한 내용은 [Class Collectors](https://docs.oracle.com/javase/8/docs/api/java/util/stream/Collectors.html){: target="_blank"}에서 확인바랍니다.<br>
