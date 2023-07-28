flex Container 안의 item들의 가로 길이가 넘치면 `가로 스크롤`을 주고 싶었다.

하지만 자꾸 가로길이를 자동으로 조절해 내가 원하는 크기가 아닌 한 화면에 다 담기도록 되던것이다.

결국 답을 찾았다.

## 📕 flex-shrink

이놈이다.

모든일의 원흉...

> item들이 컨테이너에 맞도록 줄어드는 `비율을 설정`한다. 기본값은 1이고, 0으로 설정하면 줄어들지 않는다.

![](https://velog.velcdn.com/images/dtc03003/post/8b407f02-8d47-4e71-befa-adebaa1c0aa5/image.png)

```css
flex-shrink: 0;
```

![](https://velog.velcdn.com/images/dtc03003/post/b41a6d80-5145-4264-aefd-d4e701b3af11/image.png)

-   단 `flex-wrap: wrap` 속성을 부여한 경우 적용되지 않음

-   `flex-wrap` 속성을 부여하지 않거나, `flex-wrap: nowrap" 속성을 부여해야 함

<br/>

---

<br/>

## 📕 출처

> https://conservative-vector.tistory.com/entry/CSS-flex-box-%EC%95%88-items-%ED%81%AC%EA%B8%B0%EA%B0%80-%EC%95%88-%EB%B3%80%ED%95%A0%EB%95%8C
