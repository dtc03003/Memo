# 📚 Hooks

## 📕 Hooks란?

> Hook은 React 16.8에 새로 추가된 기능, Hook은 class를 작성하지 않고도 state와 다른 React의 기능들을 사용할 수 있도록 만든 라이브러리

<br/>

### 📖 등장배경

1. Class 컴포넌트 vs Function 컴포넌트  
   hook이 나오기 전 까지는 상태값(state)에 접근, 생명주기 기능(lifecycle features)을 사용하기 위해 class형 컴포넌트 선언을 해줘야 했다.  
   함수형 컴포넌트는 한번 호출되고 메모리상에서 사라져 상태값 접근과 라이프사이클 구현이 불가능했다. 그러나 class형 컴포넌트를 사용하다보니 아래와 같은 문제점들이 발생했다

2. Class형 컴포넌트의 문제점

-   컴포넌트간에 로직의 재사용 불가능
    -   render props나 HOC와 같은 패턴을 통해 문제를 해결할 수 있지만 이러한 패턴은 코드의 추적을 어렵게 만든다
    -   계속해서 이런 코드를 사용하게 되다보면 많은 레이어들로 둘러쌓인 wrpper hell을 겪게 된다
-   코드가 복잡해진다

<br/>

### 📖 Hook의 등장

-   리액트 hook은 React 16.8버전에 새로 추가된 기능으로, 함수형 컴포넌트에서 react state와 생명주기 기능(lifecycle features)을 "연동(hook into)할 수 있게 해준다. useState를 예시로 들면 class를 사용하지 않고도 상태를 가질 수 있게 된 것.

<br/>

---

<br/>

## 📕 React Hooks 규칙

1. 같은 Hook을 여러번 호출 가능

```js
export default function App(){
  const [value1, setValue1] = useState()
  const [value2, setValue2] = useState()
  return {
    <div>
      <div>{value1}</div>
      <div>{value2}</div>
    </div>
  }
}
```

<br/>

2. 함수 컴포넌트 몸통이 아닌, 몸통 안 복합 실행문의 {}에서는 사용 불가

    javascript의 block scope는, block 외에서 사용할 수 없으므로 ( 지역변수이기 때문에 )

```js
export default function App(){
  return {
    <div>
      // 불가능
      <div>{const [value, setvalue] = useState()}</div>
    </div>
  }
}
```

3. 비동기 함수는 콜백함수로 사용 불가

```js
export default function App(){
  // useEffect Hook 내부에, 비동기 함수가 들어가므로 에러 발생
  useEffect(async () => {
    await Promise.resolve(1)
  }, [])

  return {
    <div>
      <div>Test</div>
    </div>
  }
}
```

<br/>

---

<br/>

## 📕 React에서 기본적으로 지원하는 Hooks

1. useState
    > 컴포넌트의 state(상태)를 관리 할 수 있다.  
    > 상태에 따라, 다른 화면 출력
2. useEffect
    > 렌더링 이후에 실행할 코드를 만들수 있다.  
    > 어떤 변수가 변경될때마다(의존성), 특정기능이 작동하도록 할 수 있다.
3. useContext
    > 부모컴포넌트와 자식컴포넌트 간의 변수와 함수를 전역적으로 정의할 수 있다.
4. useReducer
    > state(상태) 업데이트 로직을, reducer 함수에 따로 분리 할 수 있다.
5. useRef
    > 컴포넌트나 HTML 요소를 래퍼런스로 관리할 수 있다.
6. forwardRef
    > useRef로 만든 래퍼런스를 상위 컴포넌트로 전달할 수 있다.
7. useImperativeHandle
    > useRef로 만든 래퍼런스의 상태에 따라, 실행할 함수를 정의 할 수 있다.
8. useMemo, useCallback
    > 의존성 배열에 적힌 값이 변할 때만 값,함수를 다시 정의할 수 있다. ( 재랜더링시 정의 안함 )
9. useLayoutEffect
    > 모든 DOM 변경 후 브라우저가 화면을 그리기(render)전에 실행되는 기능을 정할 수 있다.
10. useDebugValue
    > 사용자 정의 Hook의 디버깅을 도와준다.

<br/>

---

<br/>

## 📕 useState 사용법

### 📖 state란?

> React에서 사용자의 반응에 따라, 화면을 바꿔주기(렌더링) 위해 사용되는 트리거역할을 하는 `변수`

-   React가 state를 감시하고, 바뀐 정보에 따른 화면을 표시해준다. ( state와 setState함수의 반환값을 비교 )
-   state는 어디에서나 사용가능
-   컴포넌트는 시간이 지나고, 앱이 커질수록 많이지므로 점점 관리하기 어려워지는 단점

<br/>
### 📖 state만들기

```js
// React에 기본적으로 내장되어 있는 useState 훅을 사용하면, state를 만들 수 있다.

import { useState } from "react";

// const [state, state변경함수] = useState(기본 state값);

const [isLoggedIn, setIsLoggedIn] = useState(false);
```

<br/>

### 📖 state 변경하기

```js
// 전에 만든 "isLoggedIn" state의 값을 true로 변경한다.

setIsLoggedIn(true);

// ** useState함수를 사용해 만든 "state 변경 함수"를 사용하여야 한다.
```

<br/>

---

<br/>

## 📕 useEffect 사용법

```js
// React에 기본적으로 내장되어 있는 useState와, useEffect 불러오기

import { setState, useEffect } from "react";

...

function App() {
  const [data, changeData] = setState(false)

  // useEffect(실행할 함수, 트리거가 될 변수)

  useEffect(() => {
    if (data.me === null) {
      console.log("Data changed!")
    }

    return () => console.log("컴포넌트 파괴, 언마운트 됨")
  }, [data]);

  // data변수가 바뀔때마다, react가 이를 감지해, 콘솔창에 "Data changed!" 출력

  return (
    <div>
      <button value="적용" onClick={changeData(!data)} />
    </div>
  )
}

export default App;
```

<br/>

---

<br/>

## 📕 useLayoutEffect 사용법

```js
// React에 기본적으로 내장되어 있는 useState와, useEffect 불러오기

import { setState, useLayoutEffect } from "react";

...

function App() {
  const [data, changeData] = setState(false)

  // useLayoutEffect(실행할 함수, 트리거가 될 변수)

  useLayoutEffect(() => {
    if (data.me === null) {
      console.log("Data changed!")
    }

    return () => console.log("Layout 사라짐")
  }, [data]);

  // data변수가 바뀔때마다, react가 이를 감지해, 콘솔창에 "Data changed!" 출력

  return (
    <div>
      <button value="적용" onClick={changeData(!data)} />
    </div>
  )
}

export default App;
```

### 📖 useEffect와 useLayoutEffect의 차이점

|  useEffect  |              useLayoutEffect              |
| :---------: | :---------------------------------------: |
| 비동기 방식 | 동기 방식 ( 끝날때까지 React가 기다려줌 ) |

<br/>

---

<br/>

## 📕 useContext 사용법

```js
// newContext.js

import { createContext } from "react"; // createContext 함수 불러오기

// context안에 homeText란 변수를 만들고, 공백("") 문자를 저장한다.
const newContext = createContext({
    homeText: "",
});
```

context를 사용할 부분 선택하기, 새로운 정보 저장하기

```js
// App.js

import React from "react";
import { View } from "react-native";
import Home from "./Home"; // 자식 컴포넌트 불러오기

import { newContext } from "./newContext"; // context 불러오기

export default function App() {
    // context에 저장할 정보를 입력한다.
    const homeText = "is Worked!";

    // NewContext.Provider로 우리가 만든 context를 사용할 부분을 감싸준다.
    return (
        <newContext.Provider value={{ homeText }}>
            <View>
                <Home />
            </View>
        </newContext.Provider>
    );
}
```

context 사용하기

```js
// Home.js

import React from "react";
import { Text, View } from "react-native";

import { useContext } from "react";
import { newContext } from "../newContext";


export default function Home() {

  // useContext hook 사용해서, newContext에 저장된 정보 가져오기
  const { homeText } = useContext(newContext);

  // 불러온 정보 사용하기!!
  return (
    <View>
      <Text>{homeText}<Text>
    </View>
  );
}
```

<br/>

### 📖 context 장점

-   React에서 context 없이 변수나 함수를 다른 컴포넌트로 전달하려면 부모자식간에만 전달이 가능하므로, 컴포넌트가 많아질수록 불필요한 컴포넌트를 많이 거쳐야하는 문제가 발생한다! ( A -> B -> C -> D )

-   context를 이용하면, 중간과정을 재치고 직통으로 전달할 수 있다! ( A -> D )

-   단 전달하고자하는 컴포넌트에 context를 만들면, 불필요한 호출이 추가될 수 있으므로, context 전용 파일을 만들어야 한다.

    예시 조건 )
    컴포넌트 : A, B, C, D ( A가 최상위 컴포넌트 )  
    전달 : A -> D  
    A 컴포넌트에 context 생성  
    D 컴포넌트에서 context 불러옴

    실행 과정 )

1. A가 렌더링되며, B, C, D를 차례로 불러옴
2. D에서 context를 가져오기위해 A를 다시불러옴
3. A를 다시 불러오면서, 불필요한 중복이 발생함

<br/>

---

<br/>

## 📕 useMemo 사용법

Memoization : 과거에 계산한 값을 반복해서 사용할때, 그 값을 캐시에 저장하는 것

-   재귀함수에 사용하면, 불필요한 반복 수행을 대폭 줄일 수 있다.
-   의존성을 가지므로, 첫렌더링시에만 저장할 변수를 설정할 수 있다.

```js
export default function App() {
    const data = useMemo(() => "data", []);
    // 데이터 변수는 의존성 배열 []에따라 선언된다. ( []사용시, 첫 렌더링 시에 1번만 선언 )
    return <></>;
}
```

<br/>

---

<br/>

## 📕 useCallback 사용법

useMemo의 함수버전. 반복적으로 사용되는 함수를 캐시에 저장할 수 있다.

```js
export default function App() {
    const avatarPressed = useCallback(() => Alert.alert("avatar pressed."), []);
    return <></>;
}
```

<br/>

---

<br/>

## 📕 useReducer 사용법 ( Redux 개념 )

여러개의 상태를 통합해 관리

-   state : 상태
-   action : 변화내용 객체
-   reducer : state와 action 인자로 받아, 다음 상태 반환하는 함수
-   dispatch : action을 반환하는 함수

```js
// 동시에 여러 상태값 업데이트
const onPress = () => {
  setMode('hype');
  setText('We are Hyped!');
  setRed(true);
}

// dispatch에게 인자를 전달받음
function reducer(state, action){
  // state에 이전 상태값 들어있음
  // action에 {키:값, ...} 형식의 객체(action)가 들어있음
  switch (action.type) {
    case 'hype':
      // 상태값 변환
      return {text: action.text, red: true};
    case 'carm':
      return {...state, red: false};
    default
      throw new Error('action type이 없습니다.');
  }
}

function Sence(){
  // 1번째 : reducer 함수, 2번째 : 초기 상태값
  const [state, dispatch] = useReducer(reducer, initialState);

  // dispatch 함수에 {키:값, ...} 형식의 객체를 전달
  const onChange = () => dispatch({type: 'hype', text: 'We are Hyped!'});
  const onDecrease = () => dispatch({type: 'carm'});
  ...
}
```

## 📕 출처

> https://velog.io/@niboo/React-Hooks-%EB%9E%80#hook%EC%9D%98-%EA%B7%9C%EC%B9%99  
> https://defineall.tistory.com/900#toc4
