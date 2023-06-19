# 📕This란?

> 대부분의 경우 this의 값은 함수를 호출한 방법이 결정합니다.  
> 실행하는 중 할당으로 설정할 수 없고 함수를 호출할 때 마다 다를 수 있습니다.  
> -MDN 문서-

<br/>

---

<br/>

# 📕전역 범위

> 일반적으로 `this`를 호출한다면, `this`는 `window`라는 전역 객체를 가리킴 <br/> (Node.js에서는 `Global`)

<br/>

```js
console.log(this === window); // true
```

<br/>

---

<br/>

# 📕함수 범위

> 함수 내부에서 `this`의 값은 함수를 호출한 방법에 의해 좌우됩니다.

<br/>

## 📖단순 호출

```js
function func() {
    return this;
}

func() === window; // true
```

<br/>

## 📖객체의 메소드(Method)

```js
const car = {
    name: "KIA",
    getName: function () {
        console.log(this.name);
    },
};

car.getName(); //KIA
```

```js
const car2 = {
    name: "Hyundai",
    getName: car.getName,
};

car2.getName(); // Hyundai
```

```js
const bindGetname = car2.getName.bind(car);
bindGetname(); // KIA
```

```js
const testCar = {
    name: "benz",
    getName: function () {
        console.log(this.name); // benz
        const innerFunc = function () {
            console.log(this.name); //
        };
        innerFunc();
    },
};
testCar.getName();
```

<br/>

# 참조

> https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/this > https://hanamon.kr/javascript-this%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%BC%EA%B9%8C/
