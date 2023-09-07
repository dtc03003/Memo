# 📚 setState

## 📕 setState란?

> state의 값을 변경할 때 사용하는 함수

### 📖 state란 무엇인가

간단히 말해서 state란 변수이다. 그렇다면 const, let, var이 있는데 왜 state를 사용할까

state는 일반 변수와는 다르게 값이 변하면 렌더링이 일어난다. 값이 변하게 되면 연관있는 컴포넌트를 다시 렌더링이되어 화면이 바뀌게 된다.

state는 props와 같이 컴포넌트 렌더링에 영향을 주는 데이터를 갖고 있는 객체이고, 컴포넌트 안에서 관리된다.

<br/>

### 📖 setState가 필요한 이유는?

컴포넌트는 현재의 this.state와 setState를 비교해서 업데이트가 필요한 경우에만 render 함수를 호출하는데, state값을 직접 수정하게 되면 리엑트가 render 함수를 호출

```js
// class
class Example extends React.Component {
    constructor(props) {
        super(props);
        this.state = {
            count: 0,
        };
    }

    render() {
        return (
            <div>
                <p>You clicked {this.state.count} times</p>
                <button onClick={() => this.setState({ count: this.state.count + 1 })}>
                    Click me
                </button>
            </div>
        );
    }
}

// 함수형
function Example() {
    const [count, setCount] = useState(0);

    return (
        <div>
            <p>You clicked {count} times</p>
            <button onClick={() => setCount(count + 1)}>Click me</button>
        </div>
    );
}
```

<br/>

### 📖 setState의 동작

```js
import React, { useState } from "react";

function App() {
    const [state, setState] = useState(1);

    const onClick = () => {
        setState(state + 1);
        console.log(state);
    };

    return (
        <div className="App">
            <button onClick={onClick}>+1</button>
            <p>현재 값 {state}</p>
        </div>
    );
}

export default App;
```

현재 setState는 이벤트 핸들러 내에서 비동기적이다. 위 코드는 state 값은 반영이 되지만, console에 찍힌 값은 이전 상태 값을 출력  
 React가 브라우저 이벤트가 끝날 시점에 state를 일괄적으로 업데이트하기 때문

<br/>

### 📖 state 설정은 왜 비동기로 작동하는가

state는 값이 변경되면 리렌더링이 발생한다. 그런데 변경되는 state가 많을 경우 리렌더링이 계속 일어날테고 속도도 저하될것이다.

따라서 변경된 값들을 모아 한번에 업데이트를 진행하여 렌더링을 줄이고자 배치(Batch) 기능을 사용해 비동기로 작동한다고 볼 수 있다. 배치 업데이트는 16ms 주기이다.

<br/>

---

<br/>

## 📕 출처

> https://codiving.kr/21  
> https://velog.io/@devmag/React-state-%EB%B3%80%EA%B2%BD-%EC%8B%9C-%EC%99%9C-useState-setState%EB%A5%BC-%EC%93%B0%EB%8A%94%EA%B0%80  
> https://taenami.tistory.com/49
