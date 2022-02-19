---
title: '[JavaScript] callback과 promise, async/await' 
excerpt: "callback과 promise, async/await 예제 및 차이점 소개"
categories:
    - JavaScript
tag:
    - JavaScript
    - 면접대비

author_profile: true    #작성자 프로필 출력 여부

last_modified_at: 2022-02-19 T19:00:00+09:00

toc: true   #Table Of Contents 목차 

toc_sticky: true
---

## 💻 CallBack
javascript에서는 callback 함수는 다른 함수의 매개변수로 함수를 전달하고, 어떠한 이벤트가 발생한 후 매개변수로 전달한 함수가 다시 호출되는 것을 의미합니다.<br><br>
callback의 사용 예는 아래와 같습니다.

``` javascript
const addSum = (a,b, callback) => {
    setTimeout(() => {
        if(typeof a !== 'number' || typeof b !== 'number') return callback('a, b must be numbers');
        callback(undefined, a+b);
    },3000);
};

let callback = (error, sum) => {
    if(error) return console.log({error});
    console.log({sum});
}

addSum(10,20, callback);
```

위와 같이 callback을 사용하면 특정함수를 실행시킨 결과를 다른 연산에 활용하는 등의 동기적 처리가 가능해집니다.
그러나 callback의 경우 첫번째 인자가 오류, 첫번째 인자가 없는 경우에 성공이다라는 것 등과 같은 개발자들간의 약속을 바탕으로 개발될 수 있으며,
이를 프로그래밍상으로 보장해주지 않습니다. 그렇기 때문에 호출되지 말아야할 로직이 호출되는 등의 로직 에러가 발생할 수 있고, 원인을 쉽게 찾지 못할 수 있습니다.<br>

또한 아래와 같은 callback hell이라는 현상에 맞닿을 경우 서비스의 유지보수가 상당히 까다로워질 수 있습니다.
``` javascript
// callback hell
addSum(10,10,(error1, sum1) =>{
    if(error1) return console.log({error1});
    console.log({sum1});
    addSum(sum1, 15, (error2, sum2) =>{
        if(error2) return console.log({error2});
        console.log({sum2});
        addSum(sum2, 30, (error3, sum3) => {
            /*
                ......  매번 에러와 이전 합을 체크해야하며, 코드의 depth가 점점 깊어지는 현상
            */
        });
    });
});
```

## 🔐 Promise

위와 같이 javascript의 비동기 처리를 위해 callback 패턴을 사용할 경우 callback hell이 발생하고 에러 처리가 어려워지는 단점을 보완하기 위해 Promise가 등장하였습니다.
Promise는 javascript의 비동기 처리에 사용되는 객체이며, Promise 객체가 생성된 시점에는 결과를 알 수 없는 값에 대한 대리자의 역할을 합니다.
<br><br>
Promise는 다음 3가지 중 하나의 상태값을 가집니다.
- Pending(대기) : 연산에 대한 어떤 동작도 하지 않은 초기상태
- Fulfilled(이행) : 연산을 정상적으로 완료한 상태
- Rejected(거부) : 연산을 실패한 상태

Promise의 사용 예는 아래와 같습니다.
``` javascript
const addSum = (a,b) => {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            if(typeof a !== 'number' || typeof b !== 'number') {
                reject('a, b must be numbers');
            }
            resolve(a+b);
        },3000);
    });
}

addSum(10,20)
.then((sum) => console.log({sum}))
.catch((error) => console.log({error}));    // 에러를 catch에게 일임 가능

// callback hell 개선
addSum(10,20)
.then((sum1) => addSum(sum1, 1))
.then((sum2) => addSum(sum2, 2))
.then((sum3) => addSum(sum3, 3))
.then((sum) => console.log({sum}))
.catch((error) => console.log({error}));
```
Promise를 사용하면 모든 체이닝 과정에서 발생할 수 있는 에러를 **.catch()에게 일임**하여 일괄적으로 처리가 가능합니다. 
또한 callback hell의 불편함을 개선하여 코드의 가시성이 높아져 로직의 에러를 잡는데에 유리해집니다.

## 🎈 async/await
Promise는 callback의 단점들을 많이 개선하였지만, 연산의 중간값을 상위 스코프에 저장된 변수에 저장하지 않으면 활용이 어렵다는 점 등이 있습니다.
Java와 같이 동기코드에 익숙한 개발자라면 체이닝을 통한 동기처리가 익숙하지 않을 수 있습니다. 
이를 위해 **async/await**라는 문법이 등장하였으며 개발자가 읽기 좋은 코드를 작성할 수 있게 도움을 주고 있습니다.
```javascript
const addSum = (a,b) => {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            if(typeof a !== 'number' || typeof b !== 'number') {
                reject('a, b must be numbers');
            }
            resolve(a+b);
        },3000);
    });
}

const totalSum = async() => {
    try {
        let sum1 = await addSum(10, 20);
        let sum2 = await addSum(sum1, 1);
        let sum3 = await addSum(sum2, 2);
        let sum = await addSum(sum3, 3);
        console.log({sum});   
    } catch (error) {
        if(error) console.log(error);
    } 
}
```
위와 같은 형태로 코드를 작성하면, Promise의 장점은 살리고 Java 코드와 비슷한 구조로 코드를 작성할 수 있어 개발자들이 쉽게 읽고 이해할 수 있습니다.

📌 참고<br>
<https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Promise>{: target="_blank"}<br>
