## 📕 filter

```json
{
    "data": [
        { "id": 1, "skillname": "HTML", "skillgauge": 50 },
        { "id": 2, "skillname": "CSS", "skillgauge": 50 },
        { "id": 3, "skillname": "JavaScript", "skillgauge": 50 }
    ],
    "text": [
        { "id": 1, "num": 1, "text": "항목1" },
        { "id": 1, "num": 2, "text": "항목2" },
        { "id": 1, "num": 3, "text": "항목3" },
        { "id": 2, "num": 1, "text": "항목1" },
        { "id": 2, "num": 2, "text": "항목2" },
        { "id": 2, "num": 3, "text": "항목3" }
    ]
}
```

text에 id `1`번만 추출하고 싶을때

```js
const TextList = (props) => {
    return json.text.filter((v) => v.id == props);
};

console.log(TextList(1));
```

결과

![](https://velog.velcdn.com/images/dtc03003/post/117c79a0-22e2-48bf-8585-92ef2279ebaa/image.png)

<br/>

---

<br/>

## 📕 map

```json
{
    "text": [
        { "id": 1, "num": 1, "text": "항목1" },
        { "id": 1, "num": 2, "text": "항목2" },
        { "id": 1, "num": 3, "text": "항목3" },
        { "id": 2, "num": 1, "text": "항목1" },
        { "id": 2, "num": 2, "text": "항목2" },
        { "id": 2, "num": 3, "text": "항목3" }
    ]
}
```

text에 id`1`번만 받아서 1~3번까지 화면에 표시하고 싶을때

`Texts.js`

```js
import React from "react";

const text = (props) => {
    return (
        <div>
            <p>{props.text}</p>
        </div>
    );
};

export default text;
```

main.js

```js
import Texts from "./Texts";

const Skill = (props) => {
    const textlist = json.map((v) => <Texts id={v.id} text={v.text} />);
    return(
        <div>{textlist}</div>;
    )
}
```

결과

![](https://velog.velcdn.com/images/dtc03003/post/7ba7685f-494e-493e-9b6a-c68093477730/image.png)

그러나 이런 에러가 발생한다.

![](https://velog.velcdn.com/images/dtc03003/post/fd7bbce3-83d7-42b4-bb62-009920857ddd/image.png)

> # Key 값이란?
>
> key는 엘리먼트 리스트를 만들 때 포함해야하는 특수한 문자열  
> key는 리엑트가 어떤 항목을 변경, 추가, 삭제를 할때 식별하는데 도움을 준다.

> # Key 값이 필요한 이유
>
> map을 통한 나열이지만 이 key값이 없으면 추후에 수정, 삭제 등을 할 때에 어떤 요소를 의미하는지 컴퓨터가 확인하기 어렵기 때문에 고유한 key 값을 주는것이 중요하다.

### 📖 해결

```js
const textlist = json.map((v) => <Texts id={v.id} text={v.text} key={v.num} />);
```

<br/>

---

<br/>

## 📕 출처

> https://devbirdfeet.tistory.com/113  
> https://velog.io/@jiwonyyy/ React-key-%EA%B0%92%EC%9D%B4-%ED%95%84%EC%9A%94%ED%95%9C-%EC%9D%B4%EC%9C%A0-Warning-Each-Child-in-a-list-should-have-a-unique-key-prop
> https://goddaehee.tistory.com/303
