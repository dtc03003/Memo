# 📚 Promise

## 📕 Promise란?

> 비동기 작업의 최종 완료 또는 실패

자바스크립트는 비동기 처리를 위해 콜백함수를 사용한다. 하지만 콜백을 너무 남용하면 우리가 흔히 부르는 콜백 지옥에 빠질 수 있다.

![](https://velog.velcdn.com/images/dtc03003/post/4359a267-8b02-4481-ba65-01e57fa03d8a/image.png)

에러처리도 힘들고 여러 개의 비동기 처리를 한번에 하는데 한계가 존재  
이를 보안하며 비동기 처리에 사용되는 객체를 `프로미스(Promise)`라 한다.

<br/>

---

<br/>

## 📕 Promise의 장점

-   비동기 처리 시점을 명확하게 표현할 수 있다.
-   연속된 비동기 처리 작업을 수정, 삭제, 추가하기 편하고 유연하다.
-   비동기 작업 상태를 쉽게 확인할 수 있다.
-   코드의 유지 보수성이 증가한다.

프로미스는 객체이기 때문에 생성자 함수를 호출하여 인스턴스화 가능  
프로미스 생성자 함수는 resolve와 reject함수를 인자로 전달받는 콜백함수를 인자로 전달 받음  
프로미스 인자로 전달받은 콜백 함수를 내부에서 비동기 처리 함

Promise는 비동기 처리가 성공(fulfilled) 또는 실패(rejected) 등의 상태 정보를 갖게된다.  
resolve 함수가 호출 된경우 성공된 상태이고, reject 함수가 호출 된 경우 실패 상태이게 된다.

<br/>

---

<br/>

## 📕 Promise 객체 기본 사용법

### 📖프로미스 객체 생성

Promise 객체를 생성하려면 `new`키워드와 Promise 생성자 함수를 사용하면 된다. 이때 Promise 생성자 안에 두개의 매개변수를 가진 콜백 함수를 넣게 되는데,  
`첫 번째 인수`는 작업이 성공했을 때 `성공(resolve)`임을 알려주는 객체,  
`두 번째 인수`는 작업이 실패했을 때 `실패(reject)`임을 알려주는 오류 객체

```js
const myPromise = new Promise((resolve, reject) => {
    // 비동기 작업 수행
    const data = fetch("요청할 URL");

    if (data) {
        resolve(data); // 요청이 성공하여 데이터가 있다면
    } else {
        reject("Error"); // 요청이 실패하여 데이터가 없다면
    }
});
```

작업이 성공한다면 `resolve()` 실패하면 `reject()` 메서드를 호출한다.

<br/>

### 📖 프로미스 객체 처리

이렇게 만들어진 Promise 객체는 비동기 작업이 완료된 이후에 다음 작업을 연결시켜 진행할 수 있다.  
작업 결과에 따라 `.then()`과 `.catch()`메서드 체이닝을 통해 성공과 실패에 대한 후속 처리를 진행 할 수 있다.

-   처리 성공시  
    resolve(data)를 호출하면, 바로 then()으로 이어져 `then`메서드의 콜백 함수에서 성공에 대한 추가 처리를 진행  
     호출한 `resolve()` 함수의 매개변수의 값이 `then` 메서드의 콜백 함수 인자로 들어가 `then`메서드 내부에서 프로미스 객체 내부에서 다룬 값 사용 가능

-   처리 실패시
    reject("Error")를 호출하면, 바로 `.catch()`로 이어져 `catch` 메서드의 콜백 함수에서 실패에 대한 추가 처리 진행

```js
myPromise
    .then((value) => {
        // 성공적으로 수행했을 때
        console.log("Data: ", value); // 위에서 return resolve(data)의 data값이 출력된다
    })
    .catch((error) => {
        // 실패했을 때
        console.error(error); // 위에서 return reject("Error")의 "Error"가 출력된다
    })
    .finally(() => {
        // 성공하든 실패하든 무조건 실행
    });
```

<br/>

### 📖 프로미스 함수 등록

```js
// 프로미스 객체를 반환하는 함수 생성
function myPromise() {
  return new Promise((resolve, reject) => {
    if (/* 성공 조건 */) {
      resolve(/* 결과 값 */);
    } else {
      reject(/* 에러 값 */);
    }
  });
}

// 프로미스 객체를 반환하는 함수 사용
myPromise()
    .then((result) => {
      // 성공 시 실행할 콜백 함수
    })
    .catch((error) => {
      // 실패 시 실행할 콜백 함수
    });
```

함수를 만들고 그 함수를 호출하면 프로미스 생성자를 return 함으로서, 곧바로 생성된 프로미스 객체를 함수 반환값으로 얻어 사용하는 기법이다. `재사용성`, `가독성`, `확장성`에서 유리하다.
<br/>

---

<br/>

## 📕 프로미스 3가지 상태

프로미스는 비동기 작업의 결과를 약속하는 것이다.  
new Promise() 생성자로 프로미스 객체를 생성하면, 그 비동기 작업은 이미 진행 중이고 언젠가는 성공하거나 실패할 것이다. 이러한 진행중, 성공, 실패 상태를 나타내는 것이 바로 `프로미스의 상태(state)`라고 불리운다. 쉽게 말하자면 일종의 프로미스 처리 과정이라고 보면 된다.

1. `Pending(대기)` : 처리가 완료되지 않은 상태 (처리 진행중)
2. `Fulfilled(이행)` : 성공적으로 처리가 완료된 상태
3. `Eejected(거부)` : 처리가 실패로 끝난 상태

<br/>

### 📖 Pending

대기(pending) 상태란, 말 그대로 아직 비동기 처리 로직이 `완료 되지 않은 상태`

```js
const promise = new Promise((resolve, reject) => {
    setTimeout(() => {
        resolve("처리 완료");
    }, 5000);
});
console.log(promise); // Pending (대기) 상태
```

<br/>

### 📖 Fulfilled

위의 프로미스 코드를 실행하고 5초 뒤에 실행을 하면 이행(fulfilled) 상태로 변하게 된다.  
`이행`상태를 다르게 말하면 `완료`라고 봐도 된다.

<br/>

### 📖 Eejected

resolve()를 호출함으로서 프로미스 객체 상태가 이행(fulfilled) 상태가 됬다면, 반대로 reject()를 호출하면 프로미스 객체가 실패(rejected) 상태가 된다.

```js
const promise = new Promise((resolve, reject) => {
    setTimeout(() => {
        reject("처리 실패");
    }, 5000);
});
```

<br/>

---

<br/>

## 📕 출처

> https://inpa.tistory.com/entry/JS-%F0%9F%93%9A-%EB%B9%84%EB%8F%99%EA%B8%B0%EC%B2%98%EB%A6%AC-Promise  
> https://joshua1988.github.io/web-development/javascript/promise-for-beginners/  
> https://yoo11052.tistory.com/155  
> https://poiemaweb.com/es6-promise
