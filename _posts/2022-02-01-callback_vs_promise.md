---
title: '[JavaScript] callback과 promise, async/await' 
excerpt: "callback과 promise, async/await 예제 및 차이점 소개"
categories:
    - JavaScript
tag:
    - JavaScript
    - 면접대비

author_profile: true    #작성자 프로필 출력 여부

last_modified_at: 2022-02-01 T19:00:00+09:00

toc: true   #Table Of Contents 목차 

toc_sticky: true
---

## 💻 Callback
JavaScript는 Single Thread로 동작합니다. 그럼에도 JavaScript가 병렬적으로 비동기 코드를 실행하는 것처럼 보이는 것은 비동기 처리를 외부 api에 위임하고,
완료된 작업을 event loop를 통해서 반환받고, 다시 JavaScript의 실행 영역에서 callback을 실행하기 때문입니다.<br>

