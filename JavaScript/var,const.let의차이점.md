# 📚 var, let, const 차이점

<br/>

# 📕 var

`var`키워드의 문제점은 크게 3가지 존재한다.

<br/>

## 1. 변수 중복 선언 가능하여, 예기치 못한 값을 반환할 수 있다.

```js
var a = 1;
console.log(a); // 1

var a = 2;
console.log(a); // 2
```

<br/>

## 2. 함수 레벨 스코프로 인해 함수 외부에서 선언한 변수는 모두 전역 변수로 된다.

```js
var a = 1;

if (true) {
    var a = 2;
}

console.log(a); // 2
```

<br/>

## 3. 변수 선언문 이전에 변수를 참조하면 언제나 undefined를 변환한다.

```js
console.log(a); // undefined

var a = 1;
```

<br/>

# 📕 let, const

ES6에서 나온 `let`과 `const` 키워드가 3가지 문제점을 해결했다.

<br/>

## 1. 변수 중복 선언 불가

1-1 `let`

-   `let`키워드는 `변수 재선언이 불가`하지만 `재할당은 가능`하다

```js
// 변수 선언
let a = 1;
console.log(a); // 1;

// 변수 재선언
let a = 2;
console.log(a); // Uncaught SyntaxError: Identifier 'a' has already been declared

// 변수 재할당
a = 3;
console.log(a); // 3
```

1-2 `const`

-   `const`키워드는 `변수 재선언 불가` 또 `재할당 불가`

```js
// 변수 선언
const a = 1;
console.log(a); // 1;

// 변수 재선언
const a = 2;
console.log(a); // Uncaught SyntaxError: Identifier 'a' has already been declared

// 변수 재할당
a = 3;
console.log(a); // Uncaught TypeError: Assignment to constant variable.
```

-   `선언`과 `초기화`를 동시에 진행해야한다

```js
const a;    // Uncaught SyntaxError: Missing initializer in const declaration
const a = 1
```

-   객체의 재할당은 가능하다.

```js
const a = {
    b: 2,
};
a.b = 3;

console.log(a); // {b: 3}
```

<br/>

# 📕 정리

> 변수 선언에는 기본적으로 `const` 사용, 재할당이 필요한 경우 `let`

<br/>

# 📕 참조

> https://velog.io/@bathingape/JavaScript-var-let-const-%EC%B0%A8%EC%9D%B4%EC%A0%90  
> https://www.howdy-mj.me/javascript/var-let-const
