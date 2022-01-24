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

## 💻 Stream API
Stream API는 데이터를 추상화하여 다루고 다양한 방식으로 저장된 데이터를 읽고 쓰기 위한 공통된 방법을 제공합니다.
Collection뿐만 아니라 파일에 들어있는 데이터도 Stream객체로 변환하면 동일한 방법으로 처리할 수 있습니다.

## 🎈 특징
1. Stream은 외부 반복을 통해 작업하는 컬렉션과는 달리 내부 반복을 통해 작업을 수행합니다.
2. Stream은 원본 데이터를 변경하지 않지만, Collection과는 달리 재사용이 불가능합니다.
3. Stream연산은 Filter-Map 기반의 API를 사용하여 Lazy연산을 통해 성능을 최적화합니다.
4. Stream은 parallelStream() 메소드를 통한 손쉬운 병렬 처리를 지원합니다. 

## 🌊 Stream API 연산 과정
1. Stream 생성
2. 중개연산
3. 최종연산<br>
<img src="https://user-images.githubusercontent.com/26996562/150715979-0f9dce8b-689c-4fac-a769-8baad3def0a8.png  width="200" height="400"/>

📌 참고<br>
<http://tcpschool.com/java/java_stream_concept>{: target="_blank"}<br>
