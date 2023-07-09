# 📚 CSS 단위

## 📕 CSS 단위

CSS 단위는 두가지로 나뉜다.

1. `절대 길이 단위`
2. `상대 길이 단위`

<br/>

---

<br/>

## 📕 절대 길이 단위

-   상위 요소 또는 창 크기에 관계없이 `동일한 크기`를 의미한다.
-   절대 길이 단위는 반응형을 고려하지 않는 작업에 유용하며 주로 `인쇄물`에서 많이 사용되는 방법이다.
-   `상속` 된 다른 CSS로부터 영향을 받지 않는다.

|     |                                                                |
| --- | :------------------------------------------------------------: |
| px  | 화면을 구성하는 기본이 되는 단위, 모니터의 <br/> 1dot = 1pixel |
| in  | 인치는 물리적 측정이지만 pixel에 직접 매칭됨 <br/> 1in = 96px  |
| cm  |                          1cm = 37.8px                          |
| mm  |                      1mm = 0.1cm = 3.78px                      |

<br/>

---

<br/>

## 📕 상대 길이 단위

-   상대적 길이 단위는 요소에서 상대적인 길이를 지정.
-   상대적 길이 단위는 서로 다른 기기(모니터 폭) 간에 더 잘 확장됨

|      |                                                                                              |
| ---- | :------------------------------------------------------------------------------------------: |
| em   | 글꼴을 상대적으로 표현하는 단위, 부모 요소가 갖고 있는 크기에 등배단위로 처리 ex) 2em => 2배 |
| rem  |                글꼴을 root element(html태그) 기준으로 크기에 등배단위로 처리                 |
| vw   |                                뷰포트 너비(width)의 1%로 처리                                |
| vh   |                               뷰포트 높이(height)의 1%로 처리                                |
| vmin |        현재 뷰포트 중(width와 height 중) 작은 쪽으로 선택해서 vw 혹은 vh 수치로 처리         |
| vmax |         현재 뷰포트 중(width와 height 중) 큰 쪽으로 선택해서 vw 혹은 vh 수치로 처리          |

-   vmin, vmax는 익스플로러(IE)는 작동 안됨

<br/>

### 📖 em과 rem의 차이

-   둘다 등배 단위를 뜻하는 상대적 단위
-   하지만 `em`은 `부모 크기를 기준`으로 등배 단위가 처리되고, `rem`은 `root(즉 html)를 기준`으로 등배 단위가 처리됨

ex)

```html
<!DOCTYPE html>
<html>
    <head>
        <style>
            * {
                font-size: 10px;
            }
            .em {
                font-size: 1em;
            }
            .em2 {
                font-size: 2em;
            }
            .px30 {
                font-size: 30px;
            }
            .rem {
                font-size: 1rem;
            }
        </style>
    </head>
    <body>
        <div>폰트 크기 10px 입니다.</div>
        <div class="em">폰트 크기 1em 입니다.</div>
        <div class="em2">폰트 크기 2em 입니다.</div>
        <dib class="px30">
            폰트 크기 30px 입니다.
            <div class="em">부모 30px, 폰트 크기 1em 입니다.</div>
            <div class="rem">부모 30px, 폰트 크기 1rem 입니다.</div>
        </dib>
    </body>
</html>
```

![](https://velog.velcdn.com/images/dtc03003/post/3fc93281-62a6-4be0-8b7a-ca6ae94435d0/image.png)

위와 같이 `1em`은 부모 폰트 크기와 같고, `1rem`은 `최상위 폰트` 크기와 같다.

<br/>

### 📖 vw(Viewport Width)와 vh(Viewport Height)

-   이름에서 유추할 수 있듯이 뷰포트를 기준으로 한 단위
-   뷰포트는 `보여지는 영역`, 보여지는 영역에서 얼마만큼 차지할 것인지 지정하는 단위
-   `500px` 너비인 뷰포트일때 `1vw`는 뷰포트 너비의 1% 즉 `5px`이다.
-   `850px` 너비인 뷰포트일때 `1vw`는 뷰포트 너비의 1% 즉 `8.5px`이다.

![](https://velog.velcdn.com/images/dtc03003/post/ae1db3de-715f-4554-b7d6-ce641b7c6dab/image.png)

![](https://velog.velcdn.com/images/dtc03003/post/447d13b7-d539-414f-902d-c5231bb81cc4/image.png)

위와 같이 뷰포인트 가로 길이가 변할때 폰트의 크기가 달라진다.

<br/>

---

<br/>

## 📕 참조

> https://baek.dev/post/38/  
> https://developer.mozilla.org/ko/docs/Learn/CSS/Building_blocks/Values_and_units  
> https://ossam5.tistory.com/310  
> https://nykim.work/85
