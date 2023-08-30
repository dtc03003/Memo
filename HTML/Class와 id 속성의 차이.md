# 📚 Class와 Id 속성의 차이

## 📕 Class와 Id 속성

```html
<p id="title" class="name">Meerkat</p>

<style>
    #title {
        color: white;
        font-size: 16px;
    }

    .name {
        text-align: center;
    }
</style>
```

-   `Class`를 불러올 때는 클래스명 앞에 `마침표(.)`를 찍어준다.
-   `Id`를 불러올 때는 아이디값 앞에 `샾(#)` 표시를 해준다.

<br/>

---

<br/>

## 📕 중복 사용 여부

-   `Class`는 `중복 사용이 가능`하며 동일한 클래스명을 페이지 여러 곳에 사용해도 무방
-   `Id`는 페이지에서 딱 `한번만` 사용해야 한다.

```html
<!-- 중복사용 가능 -->
<p class="name">Meerkat</p>
<p class="name">김동현</p>

<!-- 중복사용 불가능 -->
<p id="title">Meerkat</p>
<p>김동현</p>
```

<br/>

---

<br/>

## 📕 그래서 언제 씀?

> `Class` 속성은 같은 유형으로 `반복되는 태그`들을 유형별로 분류하고 싶을때  
> `Id` 속성은 태그에 `유일한 이름`을 붙이고 싶을 때

<br/>

---

<br/>

## 📕 출처

> https://heinafantasy.com/155  
> https://velog.io/@jos9187/id-%EC%86%8D%EC%84%B1%EA%B3%BC-class-%EC%86%8D%EC%84%B1%EC%9D%98-%EC%B0%A8%EC%9D%B4
