```js
const skills = [
    {
        id: 1,
        skillname: "HTML",
        skillgauge: 50,
        text: "항목1",
    },
    {
        id: 2,
        skillname: "CSS",
        skillgauge: 50,
        text: "항목1",
    },
    {
        id: 3,
        skillname: "JavaScript",
        skillgauge: 50,
        text: "항목1",
    },
    {
        id: 4,
        skillname: "React",
        skillgauge: 50,
        text: "항목1",
    },
    {
        id: 5,
        skillname: "Java",
        skillgauge: 50,
        text: "항목1",
    },
    {
        id: 6,
        skillname: "Git",
        skillgauge: 50,
        text: "항목1",
    },
    {
        id: 7,
        skillname: "MarkDown",
        skillgauge: 50,
        text: "항목1",
    },
];
```

이와같은 배열을 JSON값으로 변강하자

```js
useEffect(() => {
    let json = JSON.stringify(skills);
    console.log(json);
}, []);
```

실행시키면

```json
[
    { "id": 1, "skillname": "HTML", "skillgauge": 50, "text": "항목1" },
    { "id": 2, "skillname": "CSS", "skillgauge": 50, "text": "항목1" },
    { "id": 3, "skillname": "JavaScript", "skillgauge": 50, "text": "항목1" },
    { "id": 4, "skillname": "React", "skillgauge": 50, "text": "항목1" },
    { "id": 5, "skillname": "Java", "skillgauge": 50, "text": "항목1" },
    { "id": 6, "skillname": "Git", "skillgauge": 50, "text": "항목1" },
    { "id": 7, "skillname": "MarkDown", "skillgauge": 50, "text": "항목1" }
]
```

출력된다.
