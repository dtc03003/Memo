# This란?

> this는 자신이 속한 객체 또는 자신이 생성할 인스턴스를 가리키는 자기 참조 변수(self-reference variable)이다.
> this를 통해 자신이 속한 객체 또는 자신이 생성할 인스턴스의 프로퍼티나 메서드를 참조할 수 있다.
> this는 자바스크립트 엔진에 의해 암묵적으로 생성된다.
> this는 코드 어디서든 참조할 수 있다.
> 하지만 this는 객체의 프로퍼티나 메서드를 참조하기 위한 자기 참조 변수이므로
> 일반적으로 객체의 메서드 내부 또는 생성자 함수 내부에서만 의미가 있다.
> 함수를 호출하면 인자와 this가 암묵적으로 함수 내부에 전달된다.
> 함수 내부에서 인자를 지역 변수처럼 사용할 수 있는 것처럼, this도 지역 변수처럼 사용할 수 있다.
> 단, this가 가리키는 값, 즉 this 바인딩은 함수 호출 방식에 의해 동적으로 결정된다.
> 크게 전역에서 사용할 때와 함수안에서 사용할 때로 나눌 수 있다.

```javascript
const test = {
    prop: 42,
    func: function () {
        return this.prop;
    },
};

console.log(test.func());
// Expected output: 42
```

<br/>

# 참조

https://hanamon.kr/javascript-this%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%BC%EA%B9%8C/
