옆 스크롤바를 없애고 싶었던 나는 컨텐츠들을 `<div>`안에 넣고 크기를 조정해 스크롤바를 없앴다.

하지만 헤더에서 버튼을 클릭하면 `특정 위치로 스크롤 이동`하는데 애를 먹게 되었다.

몇시간 검색을 통해 찾은 나의 결과를 공유하고자 한다.

## 📕 .scrollTop()

> .scrollTop()은 선택한 요소의 스크롤바 수직 위치를 반환하거나 스크롤바 수직 위치를 정한다.

### 📖 문법

#### 1. .scrollTop()

> 스크롤바 수직 위치를 가져온다.

ex)

```js
$("div").scrollTop();
```

<br/>

#### 2. .scrollTop(value)

> 스크롤바 수직 위치를 정한다.

ex)

```js
$("div").scrollTop(300);
```

은 div 요소의 스크롤바 위치를 위에서 300px로 정한다.

<br/>

### 📖 애니메이션

```js
$("div").animate(
    {
        scrollTop: 0,
    },
    1000
);
```

### 📖 활용

```js
const scroll = (val) => {
    $("#Contents").animate(
        {
            scrollTop: val,
        },
        1000
    );
};
```

```js
onClick={() => {
  scroll(3200);
}}
```

## 📕 출처

> https://www.codingfactory.net/10356  
> https://19park.tistory.com/16
