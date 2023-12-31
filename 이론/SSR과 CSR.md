# 📚 SSR과 CSR

## 📕 SSR

> `Server Side Rendering` - 서버에서 렌더링 준비를 마친상태로 클라이언트에 전달하는 방식

![](https://velog.velcdn.com/images/dtc03003/post/780d6d99-bb43-4770-aa92-91c51109fe1c/image.png)

1. User가 Website 요청을 보낸다.
2. Server는 즉시 렌더링 가능한 html파일을 만든다.(리소스를 체크, 컴파일 후 완성된 html 컨턴츠로 만든다.)
3. 클라이언트에 전달되는 순간 이미 렌더링 준비가 되어있기 때문에 html은 즉시 렌더링, 그러나 사이트 자체는 조작 불가능 (JavaScript가 읽히기 전이기 때문에)
4. 클라이언트가 JavaScript를 다운
5. 다운 받아지고 있는 사이에 유저는 컨텐츠는 볼 수 있지만 사이트를 조작 X (이때의 사용자의 조작을 기억)
6. 브라우저가 JavaScript 프레임 워크를 실행.
7. JavaScript까지 성공적으로 컴파일 되었기 때문에 기억하고 있던 사용자 조작이 실행되고 이제 웹 페이지는 상호작용이 가능.

<br/>

---

<br/>

## 📕 CSR

> `Client Side Rendering` - 클라이언트에서 렌더링이 일어남, 서버는 요청을 받으면 클라이언트에 html과 JavaScript를 보내주고 클라이언트는 그것을 받아 렌더링을 시작함

![](https://velog.velcdn.com/images/dtc03003/post/1fbddfb3-ca83-4df9-9c95-704ca2c0180b/image.png)

1. User가 WebSite요청을 보냄.
2. CDN이 html파일과 Js로 접근할 수 있는 링크를 클라이언트로 보냄.
3. 클라이언트는 html과 Js를 다운로드(유저는 아무것도 볼 수 없다.)
4. 다운이 완료된 JS가 실행되고 데이터를 위한 API가 호출(유저는 placeholder를 본다.)
5. 서버가 API로부터 요청에 응답.
6. API로 부터 받아온 data를 placeholder 자리에 넣어준다. 이제 페이지는 상호작용이 가능.

<br/>

---

<br/>

## 📕 CSR과 SSR의 차이

1. 웹페이지 로딩 시간

    - 첫 페이지 로딩시간  
       `CSR`의 경우 Html, CSS, 모든 Script를 한번에 불러온다.  
       `SSR`의 경우 필요한 부분의 html과 Script들만 불러온다.  
       평균적으로 `SSR`이 더 빠르다.

    - 나머지 로딩 시간  
      첫 페이지 로딩이 끝난 후, 사이트의 다른 곳으로 이동할 때  
       `CSR`의 경우 이미 첫 페이지 로딩할 때 나머지 부분을 구성하는 부분을 받아와서 빠르다.  
       `SSR`의 경우 첫 페이지를 로딩한 과정을 다시 실행해서 더 느리다.

2. SEO 대응  
   검색 엔진은 자동화된 로봇인 `크롤러`로 웹 사이트를 읽는다.  
   `CSR`의 경우 JavaScript를 실행시켜 동적으로 컨텐츠가 생성도기 때문에 JavaScript가 실행되야 metadata가 바뀐다.  
   `SSR`의 경우 서버 사이드에서 컴파일 되어 클라이언트에 넘어오기 때문에 크롤러에 대응하기 용이하다.

3. 서버 자원 사용  
   `SSR`이 매번 서버에 요청하기 때문에 서버자원을 더 많이 사용한다.

<br/>

---

<br/>

## 📕 사용 권장

### 📖 SSR을 사용하는 경우

    - 네트워크가 느릴 때
    - SEO(검색엔진 최적화)가 필요할 때
    - 최초 로딩이 빨라야하는 사이트를 개발할 때
    - 메인 Script가 크고 로딩이 매우 느릴 때 CSR은 메인 스크립트가 로딩이 끝나면 API로 데이터 요청을 보낸다. 하지만 SSR은 한번의 요청에 아예 렌더가 가능한 페이지가 돌아온다.
    - 웹 사이트가 상호작용이 별로 없을 때

### 📖 CSR을 사용하는 경우

    - 네트워크가 빠를 때
    - 서버의 성능이 좋지 않을 때
    - 사용자에게 보여줘야하는 데이터의 양이 많을 때
    - 메인 Script가 가벼울 때
    - SEO에 상관 없을 때
    - 웹 어플리케이션에 사용자와 상호작용할 것들이 많을 때(렌더링이 되지 않아 행동을 막는 것이 경험에 유리함)

<br/>

---

<br/>

## 📕 출처

> https://velog.io/@ahsy92/%EA%B8%B0%EC%88%A0%EB%A9%B4%EC%A0%91-CSR%EA%B3%BC-SSR#%EC%82%AC%EC%9A%A9-%EA%B6%8C%EC%9E%A5
